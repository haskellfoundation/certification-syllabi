## Q: Rewrite this let expression using a where expression.

```haskell
sumNumbers xs = 
    let sumFunction x acc = x + acc
    in foldr someFunction 0 xs

-- sumNumbers xs = foldr someFunction 0 xs
--     where someFunction x acc = x + acc
```

## Q: Implement the `hiSayer` function so that prints "Hi [[person]]!" to each person in the list of people and discards the resulting list.

```haskell
sayHiToPeople people = mapM_ hiSayer people
-- sayHiToPeople people = traverse_ hiSayer people
    where 
        hiSayer :: String -> IO ()
        hiSayer = undefined
        -- hiSayer person = putStrLn $ "Hello " ++ person ++ "!"

hellos = sayHiToPeople ["Alice", "Bob", "Charlie"]
```


## Q: Use let bindings or where expressions to factor out common subexpressions

```haskell
-- Thanks Nickolay!
magicNames :: (String, String) -> [String]
magicNames (alice, bob) = reverse
 [ "magic" ++ alice , reverse ("magic" ++ bob), "magic" ++ (alice ++ bob)]

-- Answer
-- magicNames :: (String, String) -> [String]
-- magicNames (alice, bob) = reverse
--  [ magic alice , reverse (magic bob), magic (alice ++ bob)]
--   where
--     magic name = "magic" ++ name
```

```haskell



```

## Q: Use a let ... in or where expression to rewrite the function expressed in runApp

```haskell

runApp :: Monad m => a -> (b -> m c) -- Requires typechecking!
runApp a = \resp -> do
    doThing1 a resp
    doThing2 a resp

-- runApp a = app
--     where app resp = do
--         doThing1 a resp
--         doThing2 a resp

-- runApp a = let app resp = do
--                 doThing1 a resp
--                 doThing2 a resp
--             in app
```


Nested where and lets? Correct syntax: Making sure people don't do `where ... in`.