
## Q1: Rewrite this expression using guards ( | ) 

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

## Q2: Rewrite this expression using a case expression. 

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