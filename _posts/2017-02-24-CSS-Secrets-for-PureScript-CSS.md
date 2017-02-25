---
layout: post
title: CSS Secrets for PureScript CSS
date: 2017-02-24
---

PureScript compiles to JavaScript and looks really similar to Haskell. Working with it has been pretty fun due to the language and also the helpful documentation.
One opinion is that type safety should extend to styling as well. The libraries for `purescript-css` and `purescript-pux-css`
(a library similar to Redux and Elm) introduce type-safe CSS to PureScript. From the Pux docs:

>CSS can and should be composed in a type-safe manner by using purescript-css and purescript-pux-css. Purescript-css provides a monad for specifying styles, and purescript-pux-css provides the css method for rendering to tuples, and a style attribute that takes CSS directly and returns an Attribute.

While type-safety seems neat, the library is pretty slugglish and in my opinion doesn't offer more (but frequently less) than vanilla CSS. This is due to confirming each attribute's naming (some follow React's camelCase over hyhens), and creating some hacky solutions that mess with typeclasses in order to compile. For example, the `backgroundImage` property has a different typeclass than the `backgroundColor` property, which leads to limited styling of elements.

Still, once you get the hang of the syntax you can do some neat things, and have the comfort of type safety in the back of your mind. Below are a few components that show `purescript-css` syntax and what you can do with simple CSS.
 
## Box-Shadow Spread Radius
The `box-shadow` property is commonly written with three parameters and a color. There is a little-known fourth length parameter for `box-shadow`[^1] that makes the shadow larger or smaller. Because the `box-shadow` property in `purescript-css` only takes three Color values, we need to make our own function that can be applied with a fourth Color value. This will let us do a few cool things that don't work out of the box with `purescript-css` or `pux-css`, while also learning PureScript and CSS.

To start, add the fourth length parameter by importing the necessary attributes, either from the [PureScript CSS repo](https://github.com/slamdata/purescript-css/blob/v2.1.0/src/CSS/Box.purs) or with `import CSS.Box` at the top of your project file

Then, create a boxShadow function that takes a fourth parameter, rather than the existing three:

```purescript
boxShadow :: forall a. Size a -> Size a -> Size a -> Size a -> Color -> CSS
boxShadow w x y z c = 
  prefixed (browsers <> fromString "box-shadow") (w ! x ! y ! z ! c)
```

Below is markup for the Pux view and a component using our new function. Each element takes two arrays: attributes and children. Once the boxShadow function is in place, you can do several different things.

For example, creating a shadow on a single side of a box:

```purescript
  resetButton = 
   button [ style $ do
              backgroundColor (yellowgreen)
              boxShadow (0.0 # px) (5.0 # px) (4.0 # px) (-4.0 # px) (black)
          ] 
          [ text "Reset"]
```

![purescriptButtonShadow](/images/purescriptButtonShadow.png)

Or creating shadows "normally" on two adjacent sides:

```purescript
  resetButton = 
    button [ style $ do
              backgroundColor (yellowgreen)
              boxShadow (3.0 # px) (3.0 # px) (6.0 # px) (-3.0 # px) (black) 
           ] 
           [ text "Reset"]
```

Next steps can includes figuring out how to pass a list of attributes (comma seperated in vanilla CSS) to `boxShadow` to allow for shadows on oppsite sides, or multiple Glows, such as below:

![purescriptButtonBorder](/images/purescriptButtonBorder.png)

## Text Glow
Another component is one that relies on the `text-shadow` property. This lets the user create a (somewhat corny) effect of glowing text due to a small shadow the same color of the text. Note that while in vanilla CSS, the `text-shadow` property will inherit the color, but with PureScript the color must be explicitly stated.

```purescript
import CSS.Text.Shadow (textShadow)

resetButton = 
  button [ style $ do
            fontSize (1.2 # em)
            fontWeight (weight 400.0)
            backgroundColor (rgb 34 0 51)
            textShadow (0.0 # px) (0.0 # px) (0.1 # em) (rgb 34 0 51)
         ] 
         [ text "Reset"]
```

![purescriptButtonGlow](/images/purescriptButtonGlow.png)

## Source
I originaly learned this material from Lea Verou's [*CSS Secrets*](https://www.amazon.com/CSS-Secrets-Lea-Verou/dp/1449372635). It's great and my go-to for CSS.

[^1]: (`boxShadow` in PureScript)