# Lesson 08: Dictionaries

(Under Construction)

<!-- TOC depthFrom:2 -->

1. [Part A: Intro to Dicts](#part-a-intro-to-dicts)
2. [Part B: Adding Keys to a Dictionary](#part-b-adding-keys-to-a-dictionary)

<!-- /TOC -->

## Part A: Intro to Dicts

A Dictionary is another type of data structure. It is useful for when we need to map one piece of information with some value.

For example, let's say we have kept track of a list of superhero movies we have watched.

We could start with a list like so:

``` py
superhero_movies = [
    "Avengers Endgame",
    "Thor Ragnarok",
    "Antman",
    "The Dark Knight",
    "Man of Steel"
]
```

Now let's say we wanted to also know what studio these movies belonged to.

We *could* create another list to track this, and make sure they are aligned:

``` py
superhero_movie_studios = [
    "Marvel",
    "Marvel",
    "Marvel",
    "DC Comics",
    "DC Comics"
]
```

Let's say we want to find out what studio `"The Dark Knight"` belonged to:

``` py
idx = superhero_movies.index("The Dark Knight")
studio = superhero_movie_studios[idx]
```

This is tedious.

Introducing the Dictionary:

``` py
movie_studio_map = {
    "Avengers Endgame": "Marvel",
    "Thor Ragnarok": "Marvel",
    "Antman": "Marvel",
    "The Dark Knight": "DC Comics",
    "Man of Steel": "DC Comics"
}

print(movie_studio_map["The Dark Knight"])
```

**Explanation**:

- Dictionaries are defined with curly braces `{}`
- Each entry of the dictionary has a key and a value.
    - The key is to the left of the `:`
    - The value is to the right of the `:`
    - For example in `"The Dark Knight": "DC Comics"`, the movie(string) `"The Dark Knight"` is the key, and the studio(string) `"DC Comics"` is the value.
- We can quickly determine the value of a key by accessing the dictionary with `[]` brackets.
    - The syntax is: `dictionary_name[key_name] == value`

## Part B: Adding Keys to a Dictionary

``` py
movie_studio_map = {
    "Avengers Endgame": "Marvel",
    "Thor Ragnarok": "Marvel",
    "Antman": "Marvel",
    "The Dark Knight": "DC Comics",
    "Man of Steel": "DC Comics"
}

movie_studio_map["Aquaman"] = "DC Comics"
```

**Explanation**:
- If a key does not already exist in a dictionary, you can specify a value for that key using the same syntax for accessing it.


