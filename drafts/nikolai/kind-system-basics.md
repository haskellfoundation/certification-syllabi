# Kind system

## Basics

In this block we expect the following prerequisites:

- Parametric algebraic data type definitions (via `data`)
- Type class declarations (single parameter)
- Kind system basics:
  - Star (`*`) or `Type` kind
  - Kinds of type constructors (e.g. `Either`)
  - Higher-kinded types (e.g. kinds `(* -> *) -> *`)

We **do not** expect the following:

- `PolyKinds` (phantom type parameters are expected to be defaulted to `Type`)
- `ConstraintKinds` (the only concrete kind used is `Type`)

### Exercise 1 (kind of a data type definition)

For each of the following declarations, answer these questions:

1. What is the kind of the defined type constructor.
2. Give 2 example values (where possible)
  of the defined type with specific types
  (or type constructors) used for the type parameters.
3. Determine the form of a (partially applied) type constructor
  suitable for a `Functor` instance (based only on the kind),
  or specify why it is impossible.

```haskell
-- Group 1 (easier)
data A a = A a
data B a = B a (S a)
data C a b = C a (T b a) | CN
data D a b = D a
data E a = E
data F = F
```

```haskell
-- Group 1 (harder, higher-kinded)
data G f a = G (f a)
data H f g a = H (f (g a))
data I a f b = I a
data J f = J f (J f)
data K f a = KP a | KF (f (K f a))
data L r f a = L ((a -> f r) -> f r)
data M t m a = M (t m a)
```

### Exercise 2 (kind of a type class parameter)

For each of the following type class definitions:

1. Provide the kind of the type parameter.
2. Suggest a concrete type (constructor) as a potential instance of this type class.

```haskell
-- difficulty increases progressively (more or less)
class A x where
  foo :: [x] -> Either String x

class B y where
  bar :: (y -> r) -> r

class C z where
  baz :: z (y -> r) -> r

class D w where
  ding :: [w Int] -> w Bool

class F u where
  flip :: (a -> b) -> u b -> u a

class G v where
  go :: (v a -> v b) -> b x -> a x

class H t where
  halt :: Monad m => t m (Int -> b) -> b

class I s where
  idle :: s Either (->) ()

class J r where
  joke :: r (r Maybe) Int

class K q where
  klone :: q t m a -> q t (t m) (m a)

class L p where
  lake :: Functor d =>
    (m a -> m b)
    -> p a b
    -> ((m c -> m d) -> p b d -> r)
    -> r
```

### Exercise 3 (kind error in a function)

For each of the following Haskell types:

1. Specify if it is well-kinded or ill-kinded (produces a kind error).
2. If it is ill-kinded:

    1. Explain the kind error
    2. Suggest a possible fix

```haskell
a :: (an -> Bool) -> an Int -> Bool
b :: (Maybe Int -> Bool) -> f Maybe -> f Bool
c :: f (Either String) -> f (Maybe String)
d :: Maybe (f Int) -> f Maybe Int
d :: Maybe (f Int) -> f Maybe Int
e :: (a -> m b) -> t a -> m t b
f :: t (m a) -> m
g :: (a -> m Bool) -> [a] -> m []
```