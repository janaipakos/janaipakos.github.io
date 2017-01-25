---
layout: post
title: Haskell Master Notes
date: 2016-10-03
---
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
- ETA Reduction- Remove variables that are repeated on both sides of the equals sign
- Function Composition ( . )= Chain functions from the right to the left
- Function Application ( $) - Replace parentheses that end to the right. However, don't make huge composition chains; use let bindings as labels

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
- If, Then, Else- Must have all three. Can replace with guards or Maybe
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

## Abstract Algebra and Category Theory
- Monoid- `mappend` is a way to combine two elements of the same type with an operator and an identity element (think a fold). The structures are combined. For example mconcat can join Sum 2, Sum 3, Sum 4 into Sum 9, or multiply them into Sum 24. Monoids predate Semigroup even though they it is a sub class. So identity is mempty (i.e. an empty list for lists, 0 for addition, or 1 for multiplication), <> is mappend, ++ is mconcat. mconcat is preferred to ++ and <> because it is less typing (you can use mconcat [list[), and certain types of text can use mconcat but not ++. The four laws of monoids are:
    + left identity, right identity, associativity, and the definition of mconcat.
- Functors are a class of types that map a function *over* each element of a data structure, not only those limited to lists with `map`. The structure is unchanged, but the values within it may change. Functor is `fmap` and it's a pattern to use mapping over structures other than lists (such as Int, Node, Maybe). The infix version of `fmap` is `<$>`. This is similar to function application `($)` but with the mapped function `f`.
- Applicatives are a way to map over structures that have more than one or any number of elements, using `pure` for one argument and `<*>` for two or more. It is a monoidal functor that lifts a functions with its own structure over a value with its own structure. More abstractly, these arguments may also have effects, such as having the possibility of failure or different ways to succeed.
    - Handles missing values well, because you do not have to check for null using conditionals or use exception handling.
    - `fmap f x = pure f <*> x`
- Monads is an applicative type that uses `return` (another name for `pure`) and bind `>>=`. Monads use the bind function `>>=` to evaluate each expression then combine the results by applying the function f. It helps the user not have to worry about failures at any step. This is the same and using a `do` block and binding the functions to values then applying a function to the result.
- ST (State Transformers) return the function ouput as well as the changed state.
- Semigroup- The Semigroup class has only one important method, the <> operator. <> combines instances of the same type. Semigroups are similar to Monoid, except that Monoids requre an identity element for the type.

