# Questions about reading and writing the type signature.

1. What's the type signature?
```haskell
-- Q1: What is the type of `s`?
-- A1: `String` (1)
-- Q2: What is the type of `handleFileContents`?
-- A2: `String -> IO Int` (1)

readFile :: FilePath -> IO String
handleFileContents :: _ 

foo :: IO Int
foo = do
  s <- readFile "test.txt"
  handleFileContents s
```

2. Complete the function to a spec. (Will require QuickCheck/testing).
```haskell

readFile :: FilePath -> IO String

--Q1: `firstChars` is a function that will return the first character of every line a file.

firstChars :: IO [Char]
firstChars = do
  s <- readFile "test.txt"
  let res = lines s
  -- Q2: Complete this function
  -- 
```

3. Recursion & Folding
```haskell
foldr :: Foldable t => (b -> a -> b) -> t a -> b

-- We will implement a function `countChar` that counts how often a character appears in a `String`.

-- Q1: Write the type signature for this function
countChar :: _
-- A1: countChar :: Char -> String -> Int (1)

-- Q2: Implement the function using recursion.
countChar = undefined

-- Q3: `countChar` can also be implemented using a fold. 
--     Which of these `counter` functions are the right type that can be used to implement `countChar` using `foldr`?. 
-- counter :: _
-- a) (Char -> Int -> Int)
-- b) (Int -> Char -> Int)
-- c) (Char -> Int -> Char)
-- d) (Int  -> Char -> Char)

-- Q4: Implement `countCharF` using `foldr` with a `where` binding for `counter`

countChar = _todo
  where counter = _todo
```
