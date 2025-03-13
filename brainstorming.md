# Brainstorming Syllabus Topics

Dump unfiltered topic ideas here

## Core Language

### Expressions and basic syntax

Includes things like space for function application, understanding the most core operator precedence rules, etc.

Possibly includes the `.` and `$` operators.

### Types

Includes type signatures, type variables, type class constraints, etc.

### Defining your own data

* Type constructors vs data constructors
* Newtypes
* Type aliases

### Type classes

How to define them and use them

### Kinds

This could be included in the "Types" topic

### Lists, List comprehensions, etc

### Laziness

Example question:

What does the following print?

```haskell
main = do
  let nums = [1..]
  print $ take 5 nums
```

### IO, do notation

I avoided using the word "monad" here because I think beginner haskellers can
start writing code in IO without needing to have any idea what "monad" actually
means.

### Core type classes

* Functor, Monad, Applicative
* Num

## Other Potential Deep-Dive Tracks

### Lenses

### Database Libraries

### Web Frameworks
