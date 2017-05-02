---
layout: post
title: PureScript Libraries
date: 2017-03-22
---

I spent the last few days trying out different PureScript libraries and building small applications. As a reference, I have used vanilla React (without Redux) and Haskell for a few months. The PureScript syntax was pretty straightforward and similar to Haskell's, with minor differences. I think I am similar to other users in that I'd like library that meshes type safety, expressive syntax, and components. Out of the libraries I tried, Pux best fits all of these criteria.

## [PureScript React](https://github.com/alexmingoia/purescript-pux)

This is pretty much too low level to warrant using PureScript. The library follows the React API, and much of your time will be spent grappling with state.

## [Thermite](https://github.com/paf31/purescript-thermite)

Thermite is the next level up with a wrapper around React. I found it overly verbose with its `spec` typeclass and its necessary qualified imports, and limiting due to Thermite building one React component.

## [Flare](https://github.com/sharkdp/purescript-flare)

Flare is a FRP library that I think this is pretty cool and easy to read. It makes creating reactive applications pretty quick. Some of its markup is clumsy, but once you have a handle on that, I think it's a good choice for FRP thanks to its closeness to PureScript. One limiting factor is the lack of documentation.

## [Pux](https://github.com/alexmingoia/purescript-pux)

Pux is my library of choice. First is the markup, which is easier to reason about than other libraries. Pux is modeled after the Elm Architecture,
and its made of user actions, state, updates to state, and a rendered view. Pux is similar to Thermite in that it's one component with a large (basically boilerplate) render function. Aside from this easy-to-reason model is the straightforward syntax. Each HTML element is made up of two arrays: its attributes and its children. Here is how you can make a button:

```haskell
div
  --empty attributes
  []
  --array of children, each with their own attributes and children
  [ button [ onClick (const Increment) ] [ text "Increment" ]
  , span [] [ text (show state) ]
  , button [ onClick (const Decrement) ] [ text "Decrement" ]
  ]
```

Personally, I find this easy to read thanks to the lack of qualified imports found in Thermite and other libraries. In addition to its readability, passing state is intuitive and easy to pick up, especially for users of Redux or Elm.

Pux seems to be the most popular library, and it should be interesting to see how it grows alongside React and PureScript.
