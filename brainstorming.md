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
* [Phantom types](https://wiki.haskell.org/index.php?title=Phantom_type)

```haskell
-- Context: this following type declaration is structured in such a way that is can use a phantom type.
-- Q: Select the part of this declaration that can be used for the phantom type (1)
type BSMessage a = ByteString
type Score = Int
type Seed = StdGen

-- Q: Convert the type signatures of `bsToInt` and `bsToStdGen` and `getData` so that they use phantom types. (3)
bsToInt :: ByteString -> Score 
bsToInt = decode

bsToStdGen :: ByteString -> Seed
bsToStdGen = mkStdGen . decode

getData :: Connection -> (ByteString -> a) -> IO a
getData conn hdlr = hdlr <$> recvSomeData conn -- example func, idk, probably put in decent sized body.

-- probably better questions available on the market
```


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

## Question Types
* Multiple choice
* Fill in the blanks
* Build this thing
* Rewrite this
