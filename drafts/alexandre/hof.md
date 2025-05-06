# High-order functions

## Basics

In this block we expect the following prerequisites:

- Some knowledge about lambdas
- Some knowledge about currying
- Syntax behind basic function and datatypes
- Basic knowledge on parametric polymorphism

We **do not** expect the following:

- Recursion
- Higher-kinded polymorphism
- "Ad-hoc" polymorphism i.e. type-classes

### Exercise 1 (The ability to reduce expressions with HOF)

Consider the following snippet

```haskell
-- Group 1 (easier)
s :: (a -> b -> c) -> (a -> b) -> a -> c
s x y z = x(z)(y(z))

k :: x -> y -> x
k x _ = x
```

Evaluate the following expression to its normal form `s k k`.

- a) `\x y -> y`
- b) `\x y -> x`
- c) `\x -> x`
- d) `\x y -> x y`
- e) This expression do not compile due a type error.


Right answer: c)
### Exercise 2 (The ability to typecheck expressions with HOF)

Consider the function take from Prelude.

```haskell
take :: Int -> [a] -> [a]
```

Also, consider the following expression

```haskell
foo :: (Int -> [a]) -> [a]
foo f = reverse (f 5)  
```

Choose the right assertion about `foo.

- a) The value `foo take` have the type `[a]`
- b) The function `foo` do not compile.
- c) The value `foo (take 5)` have the type `[Int]`
- d) The expression `foo (flip take [])` typechecks. 
- e) The expression `foo (take [])` typechecks. 

Right answer: d)

### Exercise 3 (The ability to reduce expressions with HOF)

Consider the following function:

```haskell
-- Group 1 (easier)
foo :: (t -> t) -> t -> t
foo f x = f (f x)
```

Choose the assertion that gives the `incorrect` answer.

- a) foo reverse [1,2,3] == [1,2,3]
- b) foo id () == ()
- c) foo (foo (+1)) 5 == 9
- d) foo foo foo (+2) 3 == 35
- e) foo foo foo foo (take 1) "HASKELL" == "HA"

Right answer: e)

