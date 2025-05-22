
## Q: Rewrite this expression using guards ( | ) 

```haskell
onUserAnswer :: Char -> Maybe Bool
onUserAnswer answer =
    if answer == 'y' 
    then Just True
    else if answer == 'n'
        then Just False
        else Nothing

-- onUserAnswer answer
--     | 'y' == answer = Just True
--     | 'n' == answer = Just False
--     | otherwise = Nothing
```

## Q: Rewrite this expression using a case expression. 

```haskell
onUserAnswer :: Char -> Maybe Bool
onUserAnswer answer =
    if answer == 'y' 
    then Just True
    else if answer == 'n'
        then Just False
        else Nothing

-- onUserAnswer answer = case answer of
--   'y' -> Just True
--   'n' -> Just False
--   _ -> Nothing
```

## Q: Which of these represents the correct syntax for a method using guards ( | )?

```haskell

safeDivide x y =
    | 0 == y = Nothing
    | otherwise = Just (x / y)


safeDivide x y
    | 0 == y = Nothing
    | otherwise = Just (x / y)


safeDivide x y =
    | y == 0 = Nothing
    | otherwise = Just (x / y)

```