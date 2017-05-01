---
layout: post
title: Working with Typed CSS
date: 2017-04-12
---
Typed CSS (shown below) is a good idea that isn't without its hurdles.

```haskell
boxShadow :: forall a. Size a -> Size a -> Size a -> Size a -> Color -> CSS
boxShadow w x y z c =
  prefixed (browsers <> fromString "box-shadow") (w ! x ! y ! z ! c)
```

 While I think it's great for catching logic bugs, the time-to-learn and missing properties makes it sort of a pain to work with.

## Good

A big reason I can see needing to use typed CSS is while working with a large team on a distributed project. The team may need a set of styles to follow to ensure consistency. This can be as easy as making sure that `border` takes an `Em` type and not `Px`. Or that list items are type `Rem` and not `Em`. But ultimately I think you can use a linter for sanity-checking.

## Bad

The libraries I have the most experience in, Pux-CSS (deprecated) and PureScript-CSS, all need more contributors. Some of these libraries don't have the newest features of CSS.

For example, Pursuit, which hosts API documentation for PureScript packages, does not have any information on clearfix, flexbox, or grid layout. While missing the last item is understandable due to its freshness, the first two items are years old, and flexbox is pretty important for modern layouts.


## Workflow

The workflow is something like this:

- map out or draw page layout(s)
- create the HTML with Smolder or Blaze
- populate elements with inline styles i.e. `h1 ! style do`
- compile with errors
- look through Pursuit
  - property exists >> rename property
  - property doesn't exist >> create it or use another
- Etc

## Conclusion

While working with PureScript, for example, the process is glacially paced because a ton of CSS properties haven't made their way to PureScript-CSS yet. You can either create your own, such as the fourth "optional" value for the `box-shadow` property, or do without it. But as of now, the type safety provided isn't worth the trade-off for an expressive stylesheet. And I think this is becoming more evident to do the killing off of Pux-CSS, and the absence of typed CSS in example PureScript applications.
