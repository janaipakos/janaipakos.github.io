---
layout: post
title: Transitioning From Jeykll to Hakyll
date: 2017-01-20
---

## Building Hakyll

As of this writing, Hakyll isn't in the newest version of stack. Add Hakyll to your stack.yaml as a workaround:

```haskell
extra-deps: [
  hakyll-4.9.0.0
]
resolver: lts-7.3
```

A nightly resolver can also be used.

## Next Steps
Continue the transition.
