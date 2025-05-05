# Using infinite lists, i.e. [1..]

## Q1: Write a function using the infinite list generator [1..] to create a list of  (Int, String) pairs in the order that the list-items are given.

```haskell
enumerate :: [String] -> [(Int, String)]
enumerate people = xs 
    where 
        xs :: []
        xs = undefined
        -- xs = zip [1..] people
```

## Q2: What does this expression return?
### Multiple choice

```haskell
expression = [1, 3 ..]

-- A) A non-terminating list of all odd numbers (Y)
-- B) A repeating list of alternating 1 and 3s
-- C) A list starting with 1 and then an infinite list of 3s
```