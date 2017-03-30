---
layout: post
title: Master PureScript Notes
date: 2017-03-29
---
## Pux
- Each element constructor takes an array of *attributes* and an array of *children as properties*.
```purescript
view state = 
    div
        [attributes such as href, className]
        [children properties such as h1, h2, a, text]
```
- Generally, nest everything in one `div`
- Elements are in an array, so separate them with commas. For example:
```purescript
view state =
    div
        []
        [main [] []
        ,aside [] []
        ]
```