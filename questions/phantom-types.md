# Questions about Phantom Types

```haskell
import Network.Socket(socket, openSocket, close)

-- Context: this following type declaration is structured in such a way that is can use a phantom type.
-- Q: Select the part of this declaration that can be used for the phantom type (1)
-- A: The `a` next to BSMessage
type BSMessage a = ByteString

type Score = Int
type Seed = StdGen
data ReplayState = { getFinalScore :: Score } -- implementation unimportant

receiveSomeData :: Connection -> IO ByteString

-- Q: Convert the type signatures of `bsToScore` and `bsToStdGen` and `getData` so that they use phantom types. (3)
-- A: BSMessage Score -> Score and BSMessage Seed -> Seed
-- NOTE: Should probably have some error handling when parsing.
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

initGameReplay :: Seed -> ReplayState -- implementation unimportant
openConnection :: IO Socket -- implementation unimportant
processReplayState :: ReplayState -> StdGen -> ReplayState -- implementation unimportant

-- Q: Use the functions defined above to get the score and seed for the `ReplayState`. Finally compare the scores of the final `ReplayState` with the one made by `processReplayState`. Return True for the same and False for not. (10)

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

-- Q: Write one potential benefit of using Phantom types
-- A: Open-ended answer: "Makes it so that I can't use bsToStdGen on data received by recvScore because the phantom type tracks which data I am receiving at a certain time" or something to that line.
  
-- probably better questions available on the market
```

