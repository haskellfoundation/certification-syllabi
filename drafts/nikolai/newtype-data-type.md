# Newtype vs data vs type

## Basics

In this block we expect the following prerequisites:

- Parametric algebraic data type definitions (via `data`)
- Type class declarations (single parameter)
- Lazy evaluation (in particular, distinction between `Just undefined` and `undefined`)
- Type synonyms
- Semantic differences for `newtype` and `data` keywords
- Partial functions (`error`, `undefined`)
- Record syntax (for `data` and `newtype`)

We **do not** expect the following:

- Strictness annotations and irrefutable patterns
- Boxed vs unboxed types
- `GeneralizedNewtypeDeriving` extension
- `TypeSynonymInstances` extension

### Exercise 1 (newtype, data, and laziness)

#### Variant 1 (simple)

Consider the following snippet:

```haskell
data Pos = Pos Int

pos :: Int -> Pos
pos n
  | n > 0 = Pos n
  | otherwise = error "negative"

just123 :: Pos -> Int
just123 (Pos _) = 123

f :: Int -> Int
f n = just123 (pos n)
```

Answer the following questions about the snippet:

1. Is `f` a total function? That is, is it well-defined (always returns an `Int`) on all integers given as input?
   If no, give an example of an input, on which `f` crashes (with an `error`, a "non-exhaustive pattern" error, or any other runtime error).
2. If we change `Pos` from `data` to a `newtype`, does that affect totality of `f` in any way?
   That is, is there an input such that `f` crashes on it before the change, but works fine after, or vice versa?

#### Variant 2 (simple, with map)

Consider the following snippet:

```haskell
data Pos = Pos { getPos :: Int }

mapPos :: (Int -> Int) -> Pos -> Pos
mapPos k (Pos n) = Pos (k n)

pos :: Int -> Pos
pos n
  | n > 0 = Pos n
  | otherwise = error "negative"

just123 :: Int -> Int
just123 _ = 123

f :: Int -> Int
f n = getPos (mapPos just123 (pos n))
```

Answer the following questions about the snippet:

1. Is `f` a total function? That is, is it well-defined (always returns an `Int`) on all integers given as input?
   If no, give an example of an input, on which `f` crashes (with an `error`, a "non-exhaustive pattern" error, or any other runtime error).
2. If we change `Pos` from `data` to a `newtype`, does that affect totality of `f` in any way?
   That is, is there an input such that `f` crashes on it before the change, but works fine after, or vice versa?

#### Variant 3 (a bit more advanced)

Consider the following snippet:

```haskell
data Pos a = Pos { getPos :: a } deriving (Functor)

pos :: Num a => a -> Pos a
pos n
  | n > 0 = Pos n
  | otherwise = error "negative"

f :: [Int] -> Int
f = sum . map (getPos . fmap (const 1) . pos)
```

Answer the following questions about the snippet:

1. Is `f` a total function? That is, is it well-defined (always returns an `Int`) on all (finite) lists of integers given as input?
   If no, give an example of an input, on which `f` crashes (with an `error`, a "non-exhaustive pattern" error, or any other runtime error).
2. If we change `Pos` from `data` to a `newtype`, does that affect totality of `f` in any way?
   That is, is there an input such that `f` crashes on it before the change, but works fine after, or vice versa?

### Exercise 2 (wrapper types for units)

#### Variant 1

Identify a units conversion issue in the following code:

```haskell
type Kilometers = Double
type Miles = Double
type Hours = Double

m2km :: Miles -> Kilometers
m2km x = x * 1.609344

type Per a b = Double

mph2kmph :: Miles `Per` Hour -> Kilometers `Per` Hour
mph2kmph = m2km

type Squared a = Double

sm2skm :: Squared Miles -> Squared Kilometers
sm2skm = m2km
```

Suggest a fix, using `newtype` definitions instead of `type` synonyms:

```haskell
newtype Kilometers = Km Double
newtype Miles = M Double
newtype Hours = H Double

newtype Per a b = Per Double
newtype Squared a = Squared Double

-- conversion factor between units
newtype (a :-> b) = C Double

m2km :: Miles :-> Kilometers
m2km = C 1.609344
```

### Exercise 3 (declarations)

For each of the following definitions:

1. Identify whether the definition is valid. If no — explain why.
2. Specify whether the definition will be valid if `newtype` is replaced by `data` or `type` keyword. Explain why.

```haskell
-- group 1 (monomorphic)
newtype A = A A
newtype B = B Int
newtype C = Z Int
newtype D = Int
newtype E = E { getE :: Int }
newtype F = A Int | B String
newtype G = G { a :: Int, b :: Bool }
newtype H = H (Int, Bool)
newtype I = I Int Bool
newtype J = J
newtype K
```

```haskell
-- group 2 (monomorphic, with compound types)
newtype A = A (Double -> Either String Int)
newtype B = B (Either String Int)
newtype C = Double -> Either String Int
newtype D = Either String Int
newtype E = E { getE :: (Int -> Bool) -> Bool }
newtype F = Maybe Int
newtype G = Maybe G
```

```haskell
-- group 3 (polymorphic)
newtype A a = a
newtype B b = B b
newtype C c = C (C c)
newtype D d = D (D (D d))
newtype E a b = L a | R b
newtype F a b = Either a b
newtype G a b = G (Either a b)
newtype H a b = a -> b
newtype I a b = H (a -> b)
newtype J a b = J (J (a -> b) (b -> a))
newtype K a = String -> Maybe a
newtype L a = String -> Maybe (L a)
```

```haskell
-- group 4 (polymorphic, higher-kinded)
newtype A f = A (f (A f))
newtype B f b = B (Either b (f (B f b)))
newtype C f c = D c | E (f (C f c))
newtype D f = f (D f)
```
