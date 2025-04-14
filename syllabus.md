# 1. Core Language Fundamentals
* Syntax and basic expressions
* Types and type inference
* Pattern matching
* Guards
* Let and where bindings
* Modules and imports
* Lists and list comprehensions
* Tuples and records
* Case expressions
* Recursion
* Higher-order functions
* Lazy evaluation and non-strict semantics
* Type declarations and type aliases
# 2. Type System Mastery
* Algebraic data types (ADTs)
* Parametric polymorphism
* Typeclasses
* Defining and using custom typeclasses
* Common typeclasses: Eq, Ord, Show, Read, Enum, Bounded, Functor, Applicative, Monad
* Kind system basics (*, * -> *, etc.)
* Newtype vs data vs type
* Generalized algebraic data types (GADTs)
* Existential types
* Rank-N types
* Scoped type variables
* Functional dependencies
# 3. Functional Programming Concepts
* Pure functions
* Immutability
* Function composition and pipelines
* Currying and partial application
* Point-free style
* Folding and unfolding
* Functors, Applicatives, Monads
* Monoid, Semigroup
* Category
* Traversables and Foldables
* Lenses and optics (e.g. lens library)
# 4. Standard Libraries & Prelude
* Prelude essentials
* Data.List, Data.Maybe, Data.Either
* Data.Map, Data.Set, Data.Sequence
* Data.Text, Data.ByteString
* Control.Monad, Control.Applicative
* System.IO, Text.Read
* base library
# 5. IO & Effects
* The IO Monad
* do notation
* Reading from / writing to files
* Handling command line arguments
* Working with environment variables
* Logging and debugging tools
* Exceptions and error handling (Either, Maybe, Exception, MonadError)
* Concurrency (forkIO, STM, MVar, TVar, Async)
# 6. Tooling & Ecosystem
* GHC (Glasgow Haskell Compiler)
* Cabal (build tools)
* GHCi (REPL)
* Hoogle (documentation search)
* Haddock (documentation generator)
* HLint (linter)
* Profiling and benchmarking (criterion, weigh)
* Testing: QuickCheck, Hspec, Tasty
# 7. Dependency Management & Project Structure
* Project scaffolding
* Hackage and Stackage
* Pinning dependencies
* Package version bounds and PVP
# 8. Real-World Development
## Core Patterns
* MTL (Monad Transformer Library)
* ReaderT pattern (ReaderT r IO)
## Web Development
* WAI and Warp (web server stack)
* Servant (type-safe APIs)
* Aeson (JSON parsing/encoding)
## Databases
* Beam
* postgresql-simple
# 9. Advanced Concepts
* Category theory basics
* Fixpoints and recursion schemes
* Final tagless style
* Type-safe domain modeling
* Data encoding/decoding strategies
# 10. Testing & Quality
* Property-based testing (QuickCheck)
* Unit testing (Hspec, Tasty)
* Integration tests
* Mocking and dependency injection using monads
* Test coverage tools
# 11. Deployment & DevOps
* Building executables and libraries
* Dockerizing Haskell applications
* CI/CD integration (GitHub Actions, GitLab, etc.)
* Performance tuning
* Memory profiling
# 12. Soft Skills & Extras
* Reading GHC error messages
* Navigating and contributing to open-source Haskell projects
* Reading academic papers on functional programming
* Participating in the Haskell community (Discourse, Reddit, Matrix, GitHub)
* Writing maintainable, idiomatic Haskell
