# Decorators

(Under construction)

<!-- TOC depthFrom:2 -->

1. [Part A: A simple decorator](#part-a-a-simple-decorator)
2. [Part B: Syntactical Sugar](#part-b-syntactical-sugar)
3. [Part C: Decorating functions that have args, kwargs, and returns](#part-c-decorating-functions-that-have-args-kwargs-and-returns)
4. [Part D: A simple decorator use-case](#part-d-a-simple-decorator-use-case)
5. [Part E: `functools.wraps`](#part-e-functoolswraps)
6. [Part F: Decorators with arguments](#part-f-decorators-with-arguments)

<!-- /TOC -->

## Part A: A simple decorator

``` py
def my_function():
    print("Within the function body")

def decorate(func):
    def wrapper():
        print("Before the function is run")
        func()
        print("After the function is run")

    return wrapper

my_decorated_function = decorate(my_function)
my_decorated_function()
```

**Output**

```
Before the function is run
Within the function body
After the function is run
```

**Explaination**
- We have defined two functions in our main module scope `my_function` and `decorate`
    - `my_function` is a simple function
    - `decorate` is what we would call a "decorator"

- In `decorate()` we define *another* function.
    - Note that this function is **only accessible from within the `decorate()`** function (note the indentation and scoping)
    - You can think of this function as a variable:

        ```
            def decorate(func):
                wrapper = <A new function>
                return wrapper
        ```
    - Notice that `return wrapper` does not have `()` after `wrapper`. We are **NOT** calling the function, we are **returning a reference to that new function** which can then later be called.
    - Essentially, `decorate()` is creating a new function, and returning that new function.

- In our main module scope, we call `decorate` and capture that new function to use with `my_decorated_function = decorate(...`
    - Again, `my_decorated_function` is treated similar to a variable, except, by calling it (i.e. using it with the `()` after its name), you can perform some actions.

- The new function defined in `decorate()` takes the inputted `func` argument, and calls it within its body. But it also performs other tasks before and after the function (basic prints).
- Our decorator has **decorated the function with additional commands before/after the function itself**

## Part B: Syntactical Sugar

``` py
def decorate(func):
    def wrapper():
        print("Before the function is run")
        func()
        print("After the function is run")

    return wrapper

@decorate
def my_decorated_function():
    print("Within the function body")

my_decorated_function()
```

**Output**

Same as Part A.


**Explaination**

- This is the exact same code as-in part A.
- We are leveraging Python's decorator syntax (see [PEP-318](https://www.python.org/dev/peps/pep-0318/))
- Break-down:
    - The decorator is the `@decorate`.
    - The function **beneath** the decorator is taken in as an argument **for the decorator function**
    - Python then returns the resultant function from the decorator and assigns it to a function with the same name.
    - That is; the statement:
        ``` py
        @decorate
        def some_func
        ```
    - Is equivalent to:
        ``` py
        some_func = decorate(some_func)
        ```

## Part C: Decorating functions that have args, kwargs, and returns

``` py
def decorate(func):
    def wrapper(*args, **kwargs):
        print("Before the function is run")
        ret = func(*args, **kwargs)
        print("After the function is run")
        return ret

    return wrapper

@decorate
def my_decorated_function(some_arg, some_kwarg="World"):
    return f"Function result: {some_arg} {some_kwarg}"

print(my_decorated_function("Hello"))
```

**Output**:

```
Before the function is run
After the function is run
Function result: Hello World
```

**Explaination**:

- Remember, the `wrapper()` function defined within the decorator, is the final function we will be using in our program; this is the resultant function after decorating it.
- So, if we want to have a function that takes args/kwargs, we have to make sure that `wrapper()` also is defined with args/kwargs.
- Similarly, if we want our final resultant decorated function to return something, so too does the wrapper have to return something.
    - In this case, we just take the return value from the original function, and pass it along.

## Part D: A simple decorator use-case

``` py
import time

def timer(func):
    """Print the runtime of the decorated function"""

    def wrapper_timer(*args, **kwargs):
        start_time = time.perf_counter()

        value = func(*args, **kwargs)

        run_time = time.perf_counter() - start_time
        print(f"Finished {func.__name__!r} in {run_time:.4f} secs")
        return value
    return wrapper_timer

@timer
def complex_algorithm():
    """A very complex algorithm"""

    for i in range(10000000):
        i^2

complex_algorithm()
```

**Output**:
```
Finished 'complex_algorithm' in 0.5105 secs
```

**Explaination**:

- Our decorator starts a timer before the function is run, then ends the timer once the function is complete.
- It prints out the difference to tell us how long the decorated function takes to run.

## Part E: `functools.wraps`

``` py
import functools

def bad_decorator(func):
    def wrapperA(*args, **kwargs):
        func(*args, **kwargs)
    return wrapperA

def good_decorator(func):
    @functools.wraps(func)
    def wrapperB(*args, **kwargs):
        func(*args, **kwargs)
    return wrapperB

@bad_decorator
def without_functools():
    pass

@good_decorator
def with_functools():
    pass

print(without_functools.__name__)
print(with_functools.__name__)
```

**Output**:
```
wrapperA
with_functools
```

**Explaination**:
- We defined two silly decorators, and two useless functions
- When we print the `__name__` of the function:
    - We get `wrapperA` for the function that was decorated by the `bad_decorator`
    - We get the correct function name for the function decorated by the `good_decorator`
- `funtools.wraps()` preserves (well technically, updates) the original function name, and docstrings the function was defined with.
- Remember, decorators define new functions and returns the new function.
    - This:
        ``` py
        @decorate
        def some_func
        ```
    - Is equivalent to:
        ``` py
        some_func = decorate(some_func)
        ```
    - It follows that the original `some_func` has been overwritten with whatever `decorate` returns (in this case the wrapper)
- You should always use `functools.wraps` to ensure that the important function name and docstrings of a function are preserved

## Part F: Decorators with arguments

``` py
import time
import functools

def timer(nruns=1):
    """Print the runtime of the decorated function"""

    def decorator(func):

        @functools.wraps(func)
        def wrapper_timer(*args, **kwargs):
            start_time = time.perf_counter()

            for _ in range(nruns):
                value = func(*args, **kwargs)

            run_time = time.perf_counter() - start_time
            print(f"Finished {func.__name__!r} {nruns} times in {run_time:.4f} secs")
            return value
        return wrapper_timer
    return decorator

@timer(nruns=3)
def complex_algorithm():
    """A very complex algorithm"""

    for i in range(10000000):
        i^2

    print("Algorithm completed.")

complex_algorithm()
```

**Output**
```
Algorithm completed.
Algorithm completed.
Algorithm completed.
Finished 'complex_algorithm' 3 times in 1.5774 secs
```

**Explaination**:

- We define a decorator `timer` which takes the argument `nruns`. It is the same decorator as in [Part D](#part-d-a-simple-decorator-use-case). But it runs the wrapped function `nruns` times.
- The `timer` function **is not** a decorator, instead **it returns a decorator**.
    - To visually simplify the code:

        ``` py
        def timer(nruns=3):

            decorator = ...
            return decorator
        ```
- In the line `@timer(nruns=3)` we are calling `timer(nruns=3)`, and the return of that is then used as a decorator `@<result of timer(nruns=3)>`
    - To hammer home the point, you can do this instead:
        ``` py
        the_actual_decorator = timer(nruns=3)

        @the_actual_decorator
        def complex_algorithm(...
        ```
