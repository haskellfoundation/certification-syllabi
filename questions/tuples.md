# Tuples and records

## Q: Implement the functions frst, scnd and thrd for tuples with three items.

```haskell
-- TODO
```

## Q: The function `frst` has been given below. How does it differ from the builtin function `fst`?

```haskell
frst :: (a, b, c) -> a
frst (a, _ , _) = a

-- A) `fst` works on all tuples; frst only works with triplets
-- B) `fst` only works on tuples with two elements and `frst` works with triplets (Y)
-- C) They are the same
```

## Q: Select the relevant differences between a tuple of n elements and a list of length n elements.

```haskell
-- A) Tuples can contain elements of different types. (Y)
-- B) Tuples can be built with comprehension syntax; unlike lists
-- C) Tuples have a different type for each length; lists do not (Y)
-- D) List can be easily mapped over using e.g. fmap; tuples cannot (Y)
-- E) Tuples can easily be reversed; lists cannot.
-- F) Tuple elements can be pattern matched with (:) between the elements; Lists use (,).
```

## Q: What's the type of the following tuple? Assumed Strings are not overloaded

```haskell

ex1 = (1, "hello") -- (Int, String)

ex2 = (True, a, ['T','e','x','t']) -- (Bool, [Int], String/[Char])
        where a = [12]

ex3 = 


```

## Q: What happens if you try to create a tuple with more than two elements?

A) Syntax error: tuples cannot contain more than two elements
B) A nested tuple is created
C) The tuple is converted into a list
D) It creates a tuple with more than two elements (Y)
