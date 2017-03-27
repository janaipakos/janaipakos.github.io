---
layout: post
title: Master Idris Notes
date: 2017-03-19
---
## Types
- Enumerated types—Types defined by giving the possible values directly
    - `data Bool = False | True`
- Union types—Enumerated types that carry additional data with each value 
    - `data Shape = Triangle Double Double | Rectangle Double Double | Circle Double`
- Recursive types—Union types that are defined in terms of themselves
    - `data Nat = Z | S Nat`
- Generic types—Types that are parameterized over some other types
    - `data Either a b = Left a | Right b`
    - `data Maybe val = Nothing | Just val`
- Dependent types—Types that are computed from some other value.
    - `Vect : Nat -> Type -> Type` : The type depends on its length
    - `anyVect : (n ** Vect n String)`. The function is created kind of ad hoc once the data comes in, rather than beforehand. 

## Functions
- `span` finds the first space in an input
- `unpack` : String -> List Char converts a String into a list of characters.
- `isDigit` : Char -> Bool returns whether a Char is one of the digits 0–9.
- `all` : (a -> Bool) -> List a -> Bool returns whether every entry in a list satisfies a test.
- `cast` : cast operation? change type from one to another
- `pure` : IO wrapper for value
- `printLin` : Show a => a -> IO () displays value at console directly

## Programs
- While everything is brought together in `main`, the program is started by calling `:exec` from the repl, not `main`
- IO is an interactive program that returns a description of an IO action. Think recipe rather than execution
- Functions can be chained in the repl with bind i.e. `:exec readVect >>= printVect`