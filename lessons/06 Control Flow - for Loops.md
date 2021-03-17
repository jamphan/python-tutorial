# Lesson 06: For Loops

<!-- TOC depthFrom:2 orderedList:true -->

1. [Part A: Iterating a list.](#part-a-iterating-a-list)
2. [Part B: Iterating a `range()`](#part-b-iterating-a-range)
3. [Part C: Iterating a string](#part-c-iterating-a-string)
4. [Part D: `zip()`, Iterating two lists at the same time](#part-d-zip-iterating-two-lists-at-the-same-time)
5. [Part E: `enumerate()`, Getting the index as we enumerate](#part-e-enumerate-getting-the-index-as-we-enumerate)
6. [Part F: `continue`, skipping an iteration](#part-f-continue-skipping-an-iteration)
7. [Part G: `break`, stopping iteration](#part-g-break-stopping-iteration)

<!-- /TOC -->

## Part A: Iterating a list.

Create a file called `06a.py` and type in:

``` py
all_star_war_movies = [
    "A New Hope",
    "The Empire Strikes Back",
    "Return of the Jedi",
    "The Phantom Menace",
    "Attack of the Clones",
    "Revenge of the Sith",
    "The Force Awakens",
    "The Last Jedi",
    "The Rise of the Skywalker"
]

print("The Star Wars saga include the movies:")
for mv in all_star_war_movies:
    print("\t" + mv)
```

Now in your terminal, run the script:

```
$ python 06a.py
```

**Explanation**:

- You should see every element in the list being printed
- The `for` structure is a way for us to "iterate" through some collection of items.
    - `for mv in all_star_war_movies` translates to "*For every element in the list `all_star_war_movies`, assign that element to the variable `mv` and perform all operations within the subsequent block*"
    - Once all operations in the block are completed, we go back to the top of the `for` loop and get the next element and repeat. This is done until we have iterated every element.
- `"\t"` is called an **Escape Sequence**. This is how we tell Python we want to use some special character. In this particular case, we want to use the Tab character.
    - `\n` is the escape sequence for a newline

## Part B: Iterating a `range()`

``` py
for num in range(0,10):
    print(num)
```

**Explaination**:

- [`range(start, stop)`](https://docs.python.org/3/library/functions.html#func-range) is a built-in function that creates a list of numbers between the integers `start` and `stop` (not incl. `stop`).

**Try-out**:

- Replace `range(0,10)` with `range(0,10,2)`.
    - The optional third parameter (`2` in our case) specifies a step size, the size of the gap between each element.

## Part C: Iterating a string

``` py
for char in "Hello, World!":
    print(char)
```

**Explaination**:

- Strings are sequences of characters. Fundamentally, we would represent a String as an array of single characters.
- Because of this, we can iterate through them.

## Part D: `zip()`, Iterating two lists at the same time

``` py
listA = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h']
listB = [1, 2, 3, 4, 5, 6, 7, 8]
for aa, bb in zip(listA, listB):
    print(f"Value from A: {aa}\t Value from B: {bb}")
```

**Explanation**:

- [`zip()`](https://docs.python.org/3/library/functions.html#zip) is a built-in function that helps you iterate through many different things at the same time.
- It takes in any number of arguments, and 1 value for each arugment. So, for 3 lists: `aa, bb, cc = zip(listA, listB, listC)` and so forth.
- Using variable names like `aa` and `bb` is done to avoid using single letter variables. Using single letter variables is hard to maintain (think about if you wanted to Ctrl+F and "Replace All" the variable name). Even so, `aa` and `bb` are still bad variable names, as they don't really describe what data they're holding. At any rate, we're in a tutorial so its fine.
- The string we pass to `print()` is called an ["F-string"](https://www.python.org/dev/peps/pep-0498/), its an easy way for us to substitute expressions (e.g. variables) into our string. The string must be preceeded by the `f` character and all substitutions are done with curly braces.

## Part E: `enumerate()`, Getting the index as we enumerate

``` py
all_star_war_movies = [
    "A New Hope",
    "The Empire Strikes Back",
    "Return of the Jedi",
    "The Phantom Menace",
    "Attack of the Clones",
    "Revenge of the Sith",
    "The Force Awakens",
    "The Last Jedi",
    "The Rise of the Skywalker"
]

for idx, mv in enumerate(all_star_war_movies, start=1):
    print(f"Star Wars Episode {idx} is called {mv}")
```

**Explaination**:

- [`enumerate()`](https://docs.python.org/3/library/functions.html#enumerate) is a built-in function that provides a counter as you iterate through some iterable object (such as a list or string)
- The optional argument `start=1` tells Python to start the counter at 1 (as opposed to the default value of 0).
    - Optional arguments can be specified in the form of `key=value`, these are called Keyword arguments. It allows us to more easily tell us what information we're passing to the function as opposed to relying on the correct order of arguments.

**Try-out**:

- Try removing `start=1` (just use `enumerate(all_star_war_movies)`), notice how the numbering is off?
- Try iterating a string, e.g. `enumerate("Hello")`

## Part F: `continue`, skipping an iteration

``` py

print("The Windows versions are:")

for ii in range(100):

    if (ii < 7) or (ii == 9):
        continue

    print(f"\tWindows {ii}")
```

**Explanation**:

- The `continue` keyword tells Python to move on to the next iteration, cutting off execution in the block pre-maturely.
- In our case, when the `for` loop reaches ``ii=9``, the `if` block tells the program to continue, and move onto the next iteration ``ii=10``.

## Part G: `break`, stopping iteration

``` py

print("Numbers from 0-10:")

for ii in range(0, 100):

    if (ii > 10):
        break

    print(ii)

print("Done")
```

**Explanation**:

- `break` will stop the loop, and tell Python to move on from the for-loop