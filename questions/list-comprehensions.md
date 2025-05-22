# Using infinite lists, i.e. [1..]

## Q1: Write a function using the infinite list generator [1..] to create a list of  (Int, String) pairs in the order that the list-items are given.

```haskell
enumerate :: [String] -> [(Int, String)]
enumerate people = xs 
    where 
        xs :: []
        xs = undefined
        -- xs = zip [1..] people
        -- or equivalent
```

## Q2: What does this expression return?
### Multiple choice

```haskell
expression = [1, 3 ..]

-- A) A non-terminating list of all odd numbers (Y)
-- B) A repeating list of alternating 1 and 3s
-- C) A list starting with 1 and then an infinite list of 3s
```

### Q3: Write/select the list comprehension(s) which is equivalent to the following expression

```haskell

ex1 = [1,3,5 .. ]
-- ex1 = [ x | x <- [1,2..], (x `mod` 2) /= 0 ]

ex2 = [2,4,6 .. ]
-- ex2 = [ x | x <- [1,2..], (x `mod` 2) == 0 ]

ex3 = [7,7,7 .. ]
-- ex3, trivial, pointless, several ways: [ const 7 x | x <- [1..]]

ex4 = map (*5) [1,2,3,4,5]
-- ex4 = [ x*5 | x <- [1..5]]

ex5 xs = filter (not isVowel) xs
        where vowel x = x `notElem` "aieou"

-- ex5 xs = [ x | x <- xs, x `notElem` "aeiou" ]


ex6 = [(1,1),(1,2),(2,1),(2,2)]
-- ex6 = [(x,y) | x <- [1,2], y <- [1,2]] 
```
