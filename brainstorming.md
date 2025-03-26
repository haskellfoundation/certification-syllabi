# Brainstorming Syllabus Topics

Dump unfiltered topic ideas here

## Existing Resources

- [Learn You a Haskell](https://github.com/sdiehl/wiwinwlh)
- [Stephen Diehl's What I Wish I Knew When Learning Haskell](https://github.com/sdiehl/wiwinwlh)
- [Well-Typed Introduction to Haksell](https://teaching.well-typed.com/intro/)
- [Haskell: Uma introdução à programação funcional (Brazilian Portuguese)](https://www.casadocodigo.com.br/products/livro-haskell)

## Core Language

### Expressions and basic syntax

Includes things like space for function application, understanding the most core operator precedence rules, etc.

Possibly includes the `.` and `$` operators.

Specific examples:

- list range syntax
- list comprehensions (they're perhaps not all that common anymore, but you should still be able to read them if they appear)
- using infix operators prefix (such as `($)`) or prefix operators infix (such as `` `mod` ``)
- operator sections
- operator priority declarations (`infix` / `infixl` / `infixr`)
- pattern bindings
- `deriving`

Non-examples:

- `default` declarations (I'd arguably say you don't have to require this in "core", as they're so rare; you should probably
  still understand defaulting as a principle)

### Types

Includes type signatures, type variables, type class constraints, etc.

Specific data types:

- lists
- `Maybe`
- `Either`
- tuples
- Recursive types in general (a binary tree, for example)

Specifically, being able to:

- understand currying,
- perform type inference on a simple definition and obtain the most general type,
- reason about polymorphic types and about which type is more general than another,
- instantiate polymorphic types to specific types,
- understand about superclasses and class constraint equivalence (such as `Eq a` vs `(Eq a, Ord a)`).

Non-examples:

- understand parametricity (I think it's very useful, but I wouldn't make it a requirement)

### Defining your own data

* Type constructors vs data constructors
* Newtypes
* Type aliases

Specifically:

- the difference between `data Foo = Bar Int` and `newtype Foo = Bar Int`
- transforming a simple concept into an adequate datatype
- restrictions on type synonyms (not recursive, not partially applied)

### Type classes

How to define them and use them

More emphasis on using them for a "core exam". It is much more common in Haskell
to use existing concepts, or instantiate new datatypes to existing / common type
classes than to define ad-hoc / domain-specific type classes.

### Kinds

This could be included in the "Types" topic

I am not sure if there should be questions specifically about kinds, such as
spelling out the kinds of types, but I think it makes sense to talk about
well-formedness of types, e.g. reason about the fact that `Maybe -> Int` is
ill-formed, or `instance Functor [Int]` does not make sense.

### Lists, List comprehensions, etc

### Laziness

Example question:

What does the following print?

```haskell
main = do
  let nums = [1..]
  print $ take 5 nums
```

Specifically:

- Reasoning about termination of certain expressions
- Reasoning about the time efficiency of certain expressions
- Using `foldr` vs `foldl'` (vs `foldl`)
- Possibly, reasoning about the space efficiency of certain expressions (but this gets tricky really quickly, and probably leaves "core / basic" territory)

### IO, do notation

I avoided using the word "monad" here because I think beginner Haskellers can
start writing code in IO without needing to have any idea what "monad" actually
means.

### Core type classes

* Functor, Monad, Applicative, Monoid, Semigroup
* Num

Also (of course):

- `Eq`, `Ord`
- `Show`, `Read`
- `Bounded`, `Enum`
- `Foldable`
- `Traversable` ?

## Other Potential Topics

### Data structures

In particular:

- Performance characteristics of lists
- Finite maps, sets
- Possibly arrays / vectors (Alexandre: I don't think this is a good idea for a basic exam).

### Specific monads

- `State`, `Writer`
- `Maybe` / `Either` / `Error`

### Basic design questions

- Reasoning about / preferring totality of functions
- Use of dedicated datatypes vs strings
- Uses of eta-reduction
- ...

### Equational reasoning / laws

- Functor, Applicative and Monad laws
- Monoid and Semigroup laws
- Counterexamples: Reasoning if a given datatype is an Applicative but not a Monad, for example.


### What about language quirks?

- Monomorphism restriction?
- `Enum` instances for floats
- `Functor` / `Foldable` instances for pairs / `Either`
- ...

## Other Potential Deep-Dive Tracks

### Lenses

### Database Libraries

### Web Frameworks
