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