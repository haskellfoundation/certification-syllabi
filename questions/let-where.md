## Q: Rewrite this let expression using a where expression.

```haskell
sumNumbers xs = 
    let sumFunction x acc = x + acc
    in foldr someFunction 0 xs

-- sumNumbers xs = foldr someFunction 0 xs
--     where someFunction x acc = x + acc


compute = let 
    a = 5
    b = let
        c = 2
        in c + a
    in b * 3

-- compute = b * 3
--     where b = c + a
--           a = 5
--           c = 2

            
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
-- Thanks Nikolai!
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

## Q: Match together the functionally equivalent definitions.
(These are already paired together, scramble them, introduce inconsistencies)

```haskell
a1 x = let y = x + 1 in y * y

a2 x = y * y where y = x + 1

a3 x = (\b -> b * b)(x + 1)

--------------------------------------------------

b1 x = let 
    y = x + 5
    z = y + 5
    in (x + y + z) == 20

b2 x = (x + y + z) == 20
    where y = x + 5
          z = y + 5

--------------------------------------------------

c1 a b el = let 
    y = take 3 a ++ take 4 b
    z = drop 3 a ++ drop 4 b
    numEls =  length . filter (== el)
    in (numEls y, numEls z)

c2 a b el = (numEls y, numEls z)
    where y = take 3 a ++ take 4 b
          z = drop 3 a ++ drop 4 b
          numEls =  length . filter (== el)

--------------------------------------------------

d1 = let a = 3 + 4 in a * a
d2 = (3 + 4) * (3 + 4)
d3 = a where a = (3 + 4) * (3 + 4)

--------------------------------------------------

e1 = let x = 5 in \y -> x + y
e2 = \y -> x + y
    where x = 5

--------------------------------------------------

f1 x y = let (a, b) = (x + 1, y - 1) in a * b
f2 x y = a * b where (a, b) = (x + 1, y - 1)

--------------------------------------------------

data Person = Person { name :: String, age :: Int }

g1 x = let mkHarry = Person "Harry"
        in mkHarry x

g2 x = mkHarry x
    where mkHarry = Person "Harry"

g3 x = let namer name = Person name x
        in namer

g4 name x = Person name x

g5 x = namer
    where namer = (\f x y -> f y x) Person x
```

--------------------------------------------------

## Q: Select all of the definitions that will return the double the sum of a list of integers
```haskell 
-- These should all be correct -- obsfuscate/damage as much as needed
sum1 xs = foldr summer 0 xs
    where summer x acc = (2*x)  + acc

sum2 xs = foldr (+) 0 . doubleAll
    where doubleAll zs = fmap (*2) zs

sum3 xs = let doubled = fmap (*2) xs
           in sum doubled

sum4 xs = let twos = [2, 2 ..] -- (or repeat 2)
           in sum $ zipWith (*) twos xs

sum5 xs = sum doubled
    where doubled = [ 2 * x | x <- xs ]


sum6 xs = let 
    summed = sum xs
    in 2 * summed
```
--------------------------------------------------

## Q: Which of the following display the correct Haskell syntax (for let and where bindings) and if not correct, describe the error.

```haskell
ex1 = let x = 5
          y = x + 2
-- error needs in before `y`
-- in y = x + 2

ex2 = let x = 5; y = 2 in x * y

ex3 = let x = 4 in let y = 9 in x + y

ex4 = let x = 3 y = 4 = in x + y 
-- error requires semicolon or newline + alignment

ex5 = let x = 8
          y = 5
       in x + y * (x * y)


ex6 = let x = 6
       in y + 5
       where y = 4


ex7 xs = 10 + z
    where z = let a = filter (== 'z') xs
          z = length z
-- ERROR: z defined twice

ex7 xs = 10 + z
    where y = let a = filter (== 'z') xs
        z = length y

-- ERROR: Misalignment on definition for z


ex8 is js = let ks = map toUpper is
            where js = map toLower js
            in ks ++ js
-- ERROR: where must be used after declaration


ex9 x = y
    where y = x * x in 
```

## Q: True/False: The `in` keyword is required when using where.
-- False

## Q: When does the `in` keyword need to be used in Haskell?
A) When using `let` in a top-level function definition (Y)
B) In a do block
C) When using bind (>>=)
D) After instantiating anonymous function with (\)
E) To describe the elements of a Foldable data structure (i.e. for_ el in xs)
F) To check for membership of an item in a data structure (i.e. x in xs)
