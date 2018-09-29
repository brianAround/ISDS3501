Lesson 1: Base R
================

## R is an object oriented language: Everything is an object

  - To create an object, assign its content to an object name using `<-`
    (the assignment operator)
  - Objects that allow to perform actions on other objects are called
    functions. They are “containers” with instructions about what to do
    with other objects (e.g., `mean()`, `sum()`)
  - All functions have documentation files that can be accessed using
    `?` (e.g., `?mean()`)
  - Every function requires a minimum set of arguments to run
    successfully (e.g., `mean()` requires an argument `x`)
  - Every function has constraints about the type of object to be passed
    (e.g., `sum()` expects a vector)

## Naming rules for R objects

  - Names must start with a letter
  - Names can contain letters, digits, \_ and . (e.g., object, object1,
    object\_1, myObject, myobject, my\_object)
  - Using spaces and other symbols in objects/elements names is highly
    discouraged, but you can do it with `  ` `(backtick) like
    in`1object`or`my object\`.

## Data structures

  - Vectors (e.g., `letters`) and matrices (e.g., `matrix(letters, ncol
    = 2)`)
  - Lists and dataframes (e.g., `iris`)
  - Tibbles (because we use the tidyverse)
  - And many others we won’t look at (array, methods, etc.)

## Atomic Vectors

  - A 1D collection of homogeneous elements
  - The ultimate constitutive element of any data structure
  - Vectors’ types are for example: double, integer, logical, character

To create a vector use the `c()` function:

``` r
c(1, 2, 3, 4, 5)
## [1] 1 2 3 4 5
c(1:5)
## [1] 1 2 3 4 5
```

Two ways to declare the type of a vector:

  - Letting R coercing to the most flexible type based on your input

<!-- end list -->

``` r
typeof(c(1L, 6L, 3L))
## [1] "integer"
typeof(c("A", "character", "vector"))
## [1] "character"
typeof(c(T, TRUE, FALSE))
## [1] "logical"
```

  - Coercing using functions (`as.character()`, `as.numeric()`)

<!-- end list -->

``` r
as.integer(c(1,5,7))
## [1] 1 5 7
as.integer(str(c(1L,5L,7L)))
##  int [1:3] 1 5 7
## integer(0)
as.integer(c('2','a'))
## Warning: NAs introduced by coercion
## [1]  2 NA
```

What happens if you coherce to a “wrong” type? E.g.:
`as.integer(c('2','a'))`

### Vector type

  - What are the types of the below vectors?
  - Is `sort()` arranging the number as you expect? Why?
  - Are all the below vectors atomic (test it using `is.atomic()`)?

<!-- end list -->

``` r
sort(c("1", "2", "100", "5", "4"))
## [1] "1"   "100" "2"   "4"   "5"
sort(as.factor(c("1", "2", "100", "5", "4")))
## [1] 1   100 2   4   5  
## Levels: 1 100 2 4 5
sort(as.double(c("1", "2", "100", "5", "4")))
## [1]   1   2   4   5 100
```

### Vector indexing

You can extract elements of a vector using numeric indexing
`myVector[2]` or element(s) name(s) (e.g., `myVector['name']`). Indexing
starts at `[1]` (unlike other programming languages that sart at `0`).

Consider the following named vector:

``` r
menu <- c(pizza = '$8', lasagne = '$7.50', pasta = '$7')
```

To extract only the 1st and 3rd elements:

``` r
menu[c(1, 3)]
## pizza pasta 
##  "$8"  "$7"
```

You can use negative indexing to exclude elements from an object:

``` r
menu[-c(2:3)]
## pizza 
##  "$8"
```

## Recursive Vectors - lists

  - Lists are a 1D collection of heterogeneous elements, both in terms
    of data structure and type:

<!-- end list -->

``` r
myList <- list(1:3, "a", c(TRUE, FALSE, TRUE), list(letters, c(2, 6)))
typeof(myList)
## [1] "list"
str(myList, max.level = 1)
## List of 4
##  $ : int [1:3] 1 2 3
##  $ : chr "a"
##  $ : logi [1:3] TRUE FALSE TRUE
##  $ :List of 2
```

Most likely, we will never manipulate lists objects. However, many
functions return lists. For example, the output of fiting a linear model
`lm()` is a list:

``` r
fit <- lm(mpg ~ wt, data = mtcars)
str(fit, max.level = 0)
## List of 12
##  - attr(*, "class")= chr "lm"
```

## Exercise

Work out the exercises on a new branch of your git repo. Once you are
confident that your solutions are correct, merge the branch you created
to your master branch. Follow this workflow:

1.  Save and commit everything up to now
2.  Create a new branch and switch to it `$ git checkout -b solutions`
    (`$ git checkout [name_of_your_new_branch]` to switch between
    branches)
3.  Go back to your master `$ git checkout master` and merge it with
    `solutions` using `$ git merge solutions`
4.  After you merge, commit to master and push to GitHub

Respond to the following questions and push the responses to your
GitHub:

  - Create a character vector `family` with your family members’
name

<!-- end list -->

``` r
family <- c('Buford', 'Earlene', 'Linda', 'Chad', 'Marcia', 'Roger', 'Kenny', 'Brian', 'Laura', 'Cami', 'Mike')
```

  - Create a vector `birth` with their birth
year

<!-- end list -->

``` r
birth <- c(1930L, 1929L, 1955L, 1959L, 1961L, 1963L, 1964L, 1971L, 1971L, 1995L, 1995L)
```

  - Create another vector `age` with your family members’ ages
    (calculated using `birth`)

<!-- end list -->

``` r
age <- 2018L - birth
```

  - Use `typeof()` to make sure that `family`, `birth`, and `age` are
    the appropriate type (character, integer/double, integer/double)

<!-- end list -->

``` r
typeof(family)
## [1] "character"
typeof(birth)
## [1] "integer"
typeof(age)
## [1] "integer"
```

  - Use `names()` to name the elements of `age` with the family members’
    names from `family`

<!-- end list -->

``` r
names(age) <- family
```

  - Use inline code to print your name and age (using indexing) My name
    and age: Brian 47

  - What happens when:
    
      - You extract using a positive index bigger than the vector
        length?
    
    **Extracting a positive index larger than the vector returns a
    result of NA**
    
      - You subset by a name that doesn’t exist?
    
    **A name that doesn’t exist will also return a result of NA**
    
      - You assign a number to position 20 of the age vector?
    
    **Assigning a number to position 20 of the age vector (which before
    had only 11) created positions from 12 to 20, filling in an NA value
    for every new value below position 20, and setting postion 20 to be
    the assigned number.**

  - Read carefully the documentation for `is.vector()`. If
    `is.vector(x)` retrieves `TRUE`, does it mean that `x` is an atomic
    vector?

**No, acccording to the help text, is.vector will also produce a TRUE
response for a list.**
