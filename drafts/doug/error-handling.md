# Error Handling

```haskell
type Errors = [String]
initHeist :: Monad n => HeistConfig n -> n (Either Errors (HeistState n))
renderTemplate :: Monad n => HeistState n -> TemplateName -> Maybe (n Builder, MIMEType)
toByteString :: Builder -> ByteString

yourFunc :: HeistConfig IO -> TemplateName -> IO (Either Errors ByteString)
yourFunc hc nm = undefined
```

1. Implement `yourFunc` using the provided API.  Don't use a compiler or type
   checker.  Do everything in your head.
2. The type signatures provided above are not sufficient to get GHC to compile
   your question 1 answer.  Now add all stubs necessary to get it to compile.
   Use `undefined` as much as necessary.  You don't need the code to run, just
   compile.
