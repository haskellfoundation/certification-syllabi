
- Type declarations and type aliases
- Algebraic data types (ADTs)
- Parametric polymorphism

# Type declarations and type aliases

General ideas:

- partial application of type synonyms
- correct datatype for a specific task
- transformation between two isomorphic types
- number of distinct implementations of a given type
- infer most general type

# Type declarations and type aliases

Q: The following type declaration fails to compile and produces an error. 
What is the reason for the failure?  Describe two
different methods in which the problem can be addressed:
```
type WithExplanation a = (Explanation, a)

class HasPayload f where
  getPayload :: f a -> a 

instance HasPayload WithExplanation where
  getPayload (_explanation, a) = a
```

A: Type synonyms cannot be partially applied, so the
`instance` declaration is rejected.

Method 1: Eta-reduce the type synonym:
```
type WithExplanation = (,) Explanation
```

Method 2: Generalise the `instance` declaration:
```
instance HasPayload ((,) e) where
  ...
```

Method 3: Define a `newtype` or `data` instead:
```
data WithExplanation a = WithExplanation Explanation a

instance HasPayload WithExplanation where
  getPayload (WithExplanation _explanation a) = a
```

R: Test knowledge about the limitations of type synonyms.
Potentially tests knowledge of prefix tuple application syntax,
and partial application of tuples.

---

Q: The following code fails to compile and produces an error.
Identify the error.
Describe two different methods in which
this code can be fixed?
```
type Ints = (Int, Maybe Ints)
```

A: Type synonyms must not be recursive.

Method 1: Use a proper type instead, in this case a non-empty
list.
```
type Ints = NonEmpty Int
```

Method 2: Use a `newtype` or `data` instead:
```
data Ints = Ints Int (Maybe Ints)
```

R: Test knowledge about the limitations of type synonyms.
Potentially tests whether the intended equivalence with
non-empty lists is being recognised.

# Algebraic data types (ADTs)

Q: How many (total) values are there of the following types?
```
Maybe ()
Either Bool Bool
[Void]
```

A: In order:
```
2
4
1
```

R: Tests reasoning capabilities about the "algebra" of datatypes.

---

Q: Define a datatype that captures the concept that you want to have exactly two or
exactly three occurrences of some value of a type `a` precisely.

A:
```
data TwoOrThree a =
    Two a a
  | Three a a a
```

Another options:
```
data TwoOrThree a =
    TwoOrThree a a (Maybe a)
```

R: Tests if one can use `data` syntax. Test if one can model simple concepts as
a datatype precisely.

---

Q: A user can be identified by a phone number, an email address or both.
Define a datatype that captures this information precisely. (You can assume
suitable datatypes for phone numbers and email addresses exist.)

A:
```
data IdentificationMethod =
    OnlyPhone PhoneNumber
  | OnlyEmail EmailAddress
  | PhoneAndEmail PhoneNumber EmailAddress
```
(Another option is to use the `these` package, and the `These` type, which should
probably be fine.)

R: Tests if one can use `data` syntax. Test if one can model simple concepts as
a datatype precisely.

# Parametric polymorphism

Q: How many different total functions are there of type `Either a a` -> `Either a a`?
(And give their implementations. If you think there are too many different functions,
explain why.)

A: 4.
```
f1 (Left a)  = Left a
f1 (Right a) = Left a

f2 (Left a)  = Left a
f2 (Right a) = Right a

f3 (Left a)  = Right a
f3 (Right a) = Left a

f4 (Left a)  = Right a
f4 (Right a) = Right a
```

R: Test the understanding of basic principles of parametricity.

---

Q: If you have
```
f1 :: a -> Int -> (a, Int)
f2 :: Int -> a -> (Int, a)
```
What is the (most general / inferred) type of `[f1, f2]`? If you think it is
a type error, explain why.

A: `[f1, f2] :: [Int -> Int -> (Int, Int)]`

R: Tests basic reasoning capabilities about polymorphism and unification.

---

Q: If you have
```
f1 :: a   -> b -> (a, b)
f2 :: Int -> c
```
What is the (most general / inferred) type of `[f1, f2]`? If you think it is
a type error, explain why.

A: `[f1, f2] :: Int -> b -> (Int, b)`

R: Tests basic reasoning capabilities about polymorphism and unification.

---

Q: What is the type of `map . map`?

A: `map . map :: (a -> b) -> [[a]] -> [[b]]`

R: Tests somewhat more advanced reasoning capabilities about polymorphism and unification.
