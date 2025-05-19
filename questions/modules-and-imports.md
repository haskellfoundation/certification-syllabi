1. Importing Types vs Functions
2. Importing everything vs something
3. Importing Qualified vs Non-Qualified
4. Exporting types and functions
5. Import types non-qualified and methods qualified.

## Q: Which of the following import declarations will make the type `Text` directly available?

```haskell
-- A) import Data.Text as T(Text)
-- B) import Data.Text as T
-- C) import Data.Text (Text) (Y)
-- D) import Data.Text (Y)
-- E) import Text
```

## Q: Which of the following import declarations will make only the type `Text` directly available?

```haskell
-- A) import Data.Text as T(Text)
-- B) import Data.Text as T
-- C) import Data.Text (Text) (Y)
-- D) import Data.Text
-- E) import Text
```

## Q: Select the correct syntax for making the content of the Data.List module available

```haskell
-- A) include Data.List
-- B) using Data.List
-- C) import Data.List (Y)
-- D) from Data import List
-- E) module Data.List
```

## Q: Select the correct syntax for making available the function intercalate from Data.List

```haskell
-- A) from Data.List import intercalate
-- B) import Data.List (intercalate) (Y)
-- C) using Data.List (intercalate)
-- D) module Data.List with intercalate
-- E) with Data.List import intercalate
```

## Q: Consider the `Person` type below. Which of the following make the Person type and its constructors directly available?

```haskell
-- Person.hs

module Person where

data Person = Person { age :: Int, name :: String }

--------------

-- Main.hs

-- A) from Person.hs import Person, age, name
-- B) import Person (Person(..)) (Y)
-- C) using module Person get Person(..)
-- D) module Person with Person(name, age)
-- E) with Person import Person
-- F) import Person (Person) 
```


## Q: The function intercalate is from the module Data.List. What is the result of calling `f`?

```haskell 

import qualified Data.List as List

joinwords xss = intercalate "-" xss

f = joinwords ["We","must","be","joined","together"]

```

A) "We-must-be-joined-together"
B) "We - must - be - joined - together"
C) Compiler error
D) ["We","-","must","-","be","-","joined","-","together"]

