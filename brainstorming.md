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
import Network.Socket(socket, openSocket, close)

-- Context: this following type declaration is structured in such a way that is can use a phantom type.
-- Q: Select the part of this declaration that can be used for the phantom type (1)
-- A: The `a` next to BSMessage
type BSMessage a = ByteString

type Score = Int
type Seed = StdGen
data ParseError = ParseError
data ReplayState = { getFinalScore :: Score } -- implementation unimportant

receiveSomeData :: Connection -> IO ByteString

-- Q: Convert the type signatures of `bsToScore` and `bsToStdGen` and `getData` so that they use phantom types. (3)
-- A: BSMessage Score -> Score and BSMessage Seed -> Seed
bsToScore :: ByteString -> Score (1)
bsToScore = decode

bsToStdGen :: ByteString -> Seed (1)
bsToStdGen = mkStdGen . decode

getData :: Connection -> (ByteString -> a) -> IO a (1)
getData conn hdlr = hdlr <$> recvSomeData conn -- example func, idk, probably put in decent sized body.

-- Q: Write the functions `recvScore` and `recvSeed` using `getData`. Give appropriate type signatures to these functions. (5)

recvScore :: todo
recvScore = todo

recvSeed = todo
recvSeed = todo

------------------------

initGameReplay :: StdGen -> ReplayState
openConnection :: IO Socket -- implementation unimportant
processReplayState :: ReplayState -> StdGen -> ReplayState -- implete

Q: Use the functions defined above to get the score and seed for the `ReplayState`. Finally compare the scores of the final `ReplayState` with the one made by `processReplayState` (10)

checkReplay :: IO Bool
checkReplay = do
  conn <- openConnection
  --
  -- todo: Get score and seed
  --
  let initialState = initGameReplay _todo
      finalState = processReplayState _todo initState

  --
  -- todo: Compare scores from final state
  --

  
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
