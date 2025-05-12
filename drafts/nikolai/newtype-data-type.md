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