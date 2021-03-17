# Decorators

(Under construction)

<!-- TOC depthFrom:2 -->

1. [Part A: A simple decorator](#part-a-a-simple-decorator)
2. [Part B: Syntactical Sugar](#part-b-syntactical-sugar)
3. [Part C: Decorating functions that have args, kwargs, and returns](#part-c-decorating-functions-that-have-args-kwargs-and-returns)

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

print(my_decorated_function("Hello, "))
```

**Output**:

```
Before the function is run
After the function is run
Function result: Hello,  World
```

**Explaination**:

- Remember, the `wrapper()` function defined within the decorator, is the final function we will be using in our program; this is the resultant function after decorating it.
- So, if we want to have a function that takes args/kwargs, we have to make sure that `wrapper()` also is defined with args/kwargs.
- Similarly, if we want our final resultant decorated function to return something, so too does the wrapper have to return something.
    - In this case, we just take the return value from the original function, and pass it along.

