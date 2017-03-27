---
layout: post
title: Master Haskell Notes
date: 2016-10-03
---
Refer to [http://haskellbook.com/](http://haskellbook.com/) for more Haskell help

## GHCI Shortcuts
- : - Means "type of"
- :? - Help menu
- :load (l) - Load program
- :module (m) - Return to ghci from module. Unload module
- :set/unset - Command for changing settings. +m allows mutiline commands, +t prints type after evaluation
- :type (t) - Shows type of expression
- :kind (k) - Shows the kind of type, and can also print normalised type

## Perks of Haskell
- Strong- Does not compile with errors. Does not coerce to correct, but it does _infer_
- Static- Knows the value of each type. Don't need to declare like Java. No duck typing or replacement
- Inferred- Compiler can deduce a Type without the user declaring it

## Overview
- Polymorphic- A value is polymorphic if more than one type can have it
- Ad hoc- Ad hoc is given separate definition for type. Think of the infix + operator: it does different things
- Parametric- Value behave the same way regardless of type. Type can be used in different contexts
- Type Erasure- Haskell does not care about type when running an program, it only cares at compilation. This increases speed
- Currying- Every function has one parameter. Multi-function arguments are expressed as one argument functions. They are split or stepped through
- Partial application binds these arguments. Think of each arrow in function signatures as a new function
    + Avoid using Partial Functions (such as head, tail, init). These do not cover all possible values, such as an empty list, and can crash. Use total functions with pattern matching to cover all possible inputs
- Higher Order Functions- Functions that abstract away common patterns, such as map, filter, fold
    + Map- Do something over a list (even functions!)
    + Filter- Keep something, with a predicate or test, from a list, and throw the rest away
    + Fold- Combine lists via an operator. Use when traversing a list
        * *Catamorphism- Cata means down. Destructing data and reducing structure
        * Fold justreplaces the cons constructor in lists
        * Foldr adds the accumulator to the final element. Foldl adds the accumulator to the head*
    + Scan- Flike Fold, but shows intermediate (initial) values. I.e shows progress
- Predicate- Functions that tell if something is true. Found in list comprehension
- Record Syntax- Use curly braces for fata types instead of placeholders. E.g. Person { First :: String, Second :: String}
- Lambda Expression (anonymous function)- Binds inputs or arguments to expressions e.g. (\x -> x + 1)
    + Computes function until reaching the bottom
    + Bottom- Refers to the computation that does not result in a value. Cannot be simplified further. Another word for reducible expression.
- @ Match (`At Match`)- Pattern match a value and use it with one symbol (similar to a mixin)
- ETA Reduction- Remove vsrisbles thst are repeated on both sides of the equals sign
- Function Composition ( . )= Chain functions from the right to the left
- Funtion Application ( $) - Replace parentheses that edn to the right. However, don't make huge composition chains, use let bindings as labels

## Recursion Rules
1. Consider the type of the function
2. Determine the base or edge case along with the edge goal. Usually a empty list
3. Determine arguments. List all alternate possibilities to the goal. E.g. if not an empty list, a list with something
4. Consider the recursion or the repeated steps. What should repeat? Usually the same function
5. Ensure these actions move towards the goal. Don't waste actions

## Definitions
- Accumulator- Like recursion, but start to end rather than end to start
- Arity- The number of arguments a function or constructor takes
- Pragma- The language extension "comment" at the top of a program file

## Patterns
- If, Then, Else- 
- Case- Case {expression} of {pattern} -> result
- Pattern Match
- Guards- See if a value is true or false. Remember not to use "="
- Where/Let Bindings- let {parameter} in {binding} -> let is local and where is global
- : - Prepend to list
- !! x - get x index from list

## Algebraic Data Types
- `data BookInfo = Book Int String | Unknown`
- A data declaration, how datatypes are defined
- data- creates or defines a new Type constructor or data type
    + `data Sex = Male | Female` is an instance of constructor
- BookInfo- Type constructor, type name for datatype BookInfo
- Book- value or data constructor
- Int and String- Components, arguments, field, parameter
- Unknown- Second value or data constructor

- `"String" :: String`
- Type Signature- line of code that defines the type of a value, expression, or function
- `(++) :: [a] -> [a] -> [a]`
- 'a' is the type variable. It is polymorphic. It doesn't have to be the same literal value, only the same type.
`Type FirstName = String`
- type- keyword that introduces type synonyms. New on left, existing on right
    + new type- Allows one value or data constructor with one field
- Give functions type synonms to convey more information

- `Class class where type`
- Make own Type class without using 'deriving'
- Deriving- Type classes are tacked on to give ability (similar to an alias)
- Instance- Begins declaration of type-class instance
    + `Instance __ __ where` -> what type do you declare for the new instance. Where shows the functions

## Scope
- Haskell is lexically or location-base scoped
- Scope is the entire function, not just what is to the right of the equals. But func is outside, while let is inside

## Data Types
- Strings, or lists of Chars, are not efficient for storing data. Use Text instead with Data.Text: `import qualified Data.Text as T`
    + Similar functions between to the two, except for (++). Use mconcat or <> to concatenate
- Data.Text.IO can work with IO with Text.

## Abstract Algebra and Category Theory
- Monoid- `mappend` or `<>` is a way to combine two elements of the same type with an operator and an identity element (think fold). The structures are combined. Basically, Monoid lets you write more generic functions, such as replacing `++` with `<>` to work on Monoids as well as Strings. Can also use `mconcat` and `mempty`. `<>` is a Semigroup method that combines instances of the same type without requiring an element.

```haskell 
Sum 5 <> Sum 6 <> Sum 10 = Sum {getSum = 21}
```

- Functors are a class of types that map a function *over* each element of a data structure, not only those limited to lists with `map`. The structure is unchanged, but the values within it may change. Exposes `fmap`, with an infix as `<$>`. This is similar to function application `($)` but with the mapped function `f`.

```haskell 
fmap (+3) Just 1 = Just 4
``` 

- Applicatives are monoidal functors that lift a structured function over a structured value. `pure` inserts a value into a structure. Can take any number of elements, `pure` for one argument and `<*>` for two or more. These arguments may also have effects, such as having the possibility of failure or different ways to succeed.
    - `Nothing` handles missing values well, because you do not have to check for null using conditionals or use exception handling.

```haskell 
fmap f x = pure f <*> x
fmap (*) (Just 3) <*> (Just 2) = Just 15
pure (*) <*> (Just 3) <*> (Just 2) = Just 15
(*) <$> (Just 5) <*> (Just 3) = Just 15
```

- Monad is an applicative type that uses `return` (another name for `pure`) and the `bind` function `>>=` to evaluate a structured expression, then combine the results to return a structured function. It helps the user not have to worry about failure at any step. Can use a `do` block to bind functions to values then apply a function to the result.

```haskell
structuredSquare x = if x == 2 then Just 4 else Nothing
Just 2 >>= structuredSquare = Just 4
Just 1 >>= structuredSquare = Nothing
```

- Functions with M appended to them (mapM) are used for IO Actions with the normal ability of the function.
- ST (State Transformers) return the function ouput as well as the changed state.

- Reader is a way of stringing functions together when all those functions are awaiting one input from a shared envi- ronment.

## I/O and Working with State
- `main :: IO ()` is a empty tuple, and main is similar type to Maybe. They are both 'nothing'.
- main is not a function, because it does not return a value. It is an IO Action--a function which does not either returns no value, takes no input, or returns different value for same input.
- putStrLn is also an IO Action, because it does not return a value.
- A difference with Maybe and IO is what can go wrong. Maybe can only be Just or Nothing. But with IO, the 'nothings' are endless. So Maybe can be used outside IO, but main is contained within IO. 

## Reading and Writing Files
- System.IO lets you work with files
- Open and close files with handler hClose. Write with hPutStrLn. Check for end of file for dynamic IO with HisEOF.
- openFile has read and write mode. But use readFile and appendFile instead.

# Misc
- `liftA` == `liftM` == `fmap`
- `liftA2` == `zipWith` (only broader than only lists)
- Newtypes must have the same underlying representation as the type they wrap as the newtype wrapper disappears at compile time. So the function contained in the newtype must be isomorphic to the type it wraps. That is, there must be a way to go from the newtype to the thing it wraps and back again without losing information. 
- A parser combinator is a higher-order function that takes parsers as input and returns a new parser as output. You may remember our brief discussion of combinators way back in the lambda calculus chapter. Combinators are expressions with no free variables
- Free vvaraiable is a variable that is not bound. For example in a lambda expression, `\x -> x y`, y is a free variable.
- In the sequencing operator `(>>)`, the value gets thrown away but the effect gets passed. Compare this to bind `(>>=)`, which passes the value
- parseString takes three values: the char you are looking for (and this can be chained with `>>` and looks like `char 'a'` or `string "abc"`), `mempty` as the empty list, and a string to search
- Alternative typelcass has <|>, which is like a either or thing, some (which is one or more), and more (which is zero or more)


## Language Extensions
- OverLoadedStrings: `ghc text.hs -XOverloadedStrings` or `{-# LANGUAGE <Extension Name> #-}`. Can use Strings with Text
- ViewPatterns: Pattern matching
- TemplateHaskell: Metaprogramming
- DuplicateRecordFields: Can usse same field name with different types for record Syntax
- NoImplicitPrelude: Use custom rather than default Prelude