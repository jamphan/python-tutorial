# Exercises

<!-- TOC -->

1. [Exercises](#exercises)
    1. [Ex01. Introduction](#ex01-introduction)
    2. [Ex02. Python Interpreter](#ex02-python-interpreter)
    3. [Ex03. Variables](#ex03-variables)
        1. [Part 1: Basics](#part-1-basics)
        2. [Part 2 (OT): User input](#part-2-ot-user-input)
    4. [Ex04. Control Flow 1: `if`](#ex04-control-flow-1-if)
        1. [Designing Control Flow](#designing-control-flow)
        2. [Activities](#activities)
    5. [Ex05. Data Structure 1: Arrays](#ex05-data-structure-1-arrays)
    6. [Ex06. Control Flow 2: `for`](#ex06-control-flow-2-for)
    7. [Ex07. Checkpoint](#ex07-checkpoint)
    8. [Ex08. Data Structures 2: `dict`](#ex08-data-structures-2-dict)
    9. [Ex09. Control Flow 3: While loops](#ex09-control-flow-3-while-loops)
    10. [Ex10. Control Flow 4: Break, Continue and pass](#ex10-control-flow-4-break-continue-and-pass)
    11. [Ex11. Functions 1: Basics](#ex11-functions-1-basics)
    12. [Ex12. Functions 2: args, kwargs](#ex12-functions-2-args-kwargs)
    13. [Ex13. Applications: File I/O](#ex13-applications-file-io)
    14. [Ex14. Exceptions](#ex14-exceptions)
    15. [Ex15. Modules](#ex15-modules)

<!-- /TOC -->

## Ex01. Introduction

1. VS-Code GUI tour
    - How to read markdown
    - Keyboard shortcuts
    - `Ctrl+Shift+P`
    - Opening folders
    - Settings `ctrl+,`

2. Command line crash course
    - What is it
    - Basic file navigation (`cd`, `ls`)
    - Basic file modification (`mv`, `cp`, `rm`)

## Ex02. Python Interpreter

- Loading the interpreter
- Doing basic maths
- Commands saved in a `.py` file

## Ex03. Variables

- Motivation for variables
- Appreciation for data types (`'a' + 1` will throw `TypeError`)

### Part 1: Basics
- Overview of the core types and basic arithmetic:
    - Integers
    - Floats
    - Strings
        - Concatenation (`+`)
    - Booleans
        - Conditionals (`>`, `<`, `==`, `!=`)

- Variable naming rules
- Using variables:

``` py
my_name = "jamie"
my_last_name = "phan"
print(my_name + ' ' + my_last_name)
```

### Part 2 (OT): User input
- Getting input; `userInput = input()`

## Ex04. Control Flow 1: `if`

- Motivation for `if`
- Syntax: `if (boolean):`
    - Comment on Indentation syntax
    - Comment on scoping
    - Stress on boolean evaluation
- `else:`
- `if (boolean)`, `elif (boolean)`
- Expected execution order:

``` py
age = 25

if (age > 10):
    print("You're a teenager")
elif (age > 19):
    print("You're a young adult")
elif (age > 25):
    print("You're probably having a mid-life crisis right now")
else:
    print("You're getting old")
```

### Designing Control Flow
- Multiple `ifs` vs `if-elif`
- Integers as booleans
- `and` and `or`

``` py
age, gender = 25, "M"

if (age > 30 and gender == 'F'):
    print("Ma'am")
elif (age > 30 and gender == 'M'):
    print("Sir")
elif (age > 19):
    print("Dude")
elif (age > 10 and gender == 'F'):
    print("Girl")
elif (age > 10 and gender == 'M'):
    print("Boy")
else:
    print("Child")
```

### Activities
- Basic Q/A program
- Nesting; is there a better way of typing this code?
- Ternary operator

## Ex05. Data Structure 1: Arrays

- Motivation for arrays
    - Comment on data structures vs data types
    - importances of data structures
- Making an array `marvel_movies = ["Avengers Endgame", "Thor Ragnarok", "Antman", "Batman"]`
- Indexing arrays:
    - Zero-index
    - IndexError
    - Splicing
- Basic operations
    - Comment on 'dot' operators
        - Each type/structure has its own set of dot-operators
        - Using reference: https://docs.python.org/3/library/stdtypes.html#mutable-sequence-types
    - `.append()`
    - `.extend()`
    - `.pop()`
    - `.remove()`
    - `.sort()`
    - `.find()`
- Checking membership with `in` and `not in`

## Ex06. Control Flow 2: `for`

- Motivation for `for` loops
- Syntax: `for mv in marvel_movies:`

``` py
marvel_movies = ["Avengers Endgame", "Thor Ragnarok", "Antman"]

for mv in marvel_movies:
    print("{:s} is a marvel movie".format(mv))
```

- Challenge: Count how many movies there are in the list
- `range()`
- Comment on 'iterator' concept
    - Strings have `__iter__`

## Ex07. Checkpoint

## Ex08. Data Structures 2: `dict`

1. Motivation:
    - segway: bad data structure design won't let us easily find information about if a movie is from marvel or not
2. Explaining what a dictionary is
    - A mapping
    - Similar to a 2-col table
3. Making a dictionary

    ``` py
    movie_to_studio = {
        "Avengers Endgame": "Marvel",
        "Thor Ragnarok": "Marvel",
        "Antman": "Marvel",
        "The Dark Knight": "DC Comics",
        "Man of Steel": "DC Comics"
    }
    ```

4. Using the dictionary:

    ``` py
    print(movie_to_studio['Avengers Endgame'])
    ```

5. KeyError

    ``` py
    movie_to_studio['Resident Evil']
    ```

6. Modifying the dictionary:

    ``` py
    movie_to_studio['Resident Evil'] = 'Capcom'
    ```

7. Iterating through a dictionary:

    ``` py
    for mv in movie_to_studio:
        print(mv)

    for mv, studio in movie_to_studio.items():
        print("{:s} was produced by the {:s} studio".format(mv, studio))
    ```

8. Challenge: Count how many Marvel movies there are
9. Challenge: Count how many movies each studio has

## Ex09. Control Flow 3: While loops
## Ex10. Control Flow 4: Break, Continue and pass
## Ex11. Functions 1: Basics

1. Basic repeated code
2. Arguments
3. Returning
4. Function annotations

## Ex12. Functions 2: args, kwargs
## Ex13. Applications: File I/O
## Ex14. Exceptions

1. What are they
2. Standard Exceptions
3. Try/Catch

## Ex15. Modules
