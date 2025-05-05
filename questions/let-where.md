## Q1: Rewrite this let expression using a where expression.

```haskell
sumNumbers xs = 
    let sumFunction x acc = x + acc
    in foldr someFunction 0 xs

-- sumNumbers xs = foldr someFunction 0 xs
--     where someFunction x acc = x + acc
```

## Q2: Implement the `hiSayer` function so that says "Hi [[person]]!" to each person in the list of people.

```haskell
sayHiToPeople people = traverse_ hiSayer people
    where 
        hiSayer :: String -> IO ()
        hiSayer = undefined
        -- hiSayer person = putStrLn $ "Hello " ++ person ++ "!"

hellos = sayHiToPeople ["Alice", "Bob", "Charlie"]
```


Let and where binding questions seem difficult to implement as they can easily end up testing other parts of the language if not tightly focused on showing that let and where are interchangeable.