---
layout: post
title: Setting Up a Haskell Project
date: 2016-09-07T00:00:00.000Z
---

I haven't found the perfect Haskell IDE yet. Atom and Sublime both have alright. Testing is done through `hlint` and there is GHC support in both. Unfortunately, I have had bad luck getting `stylish-haskell` to run in either. Nevertheless, Atom is my preferred, through its packages `language-haskell`, `ide-haskell`, and `haskell-ghc-mod`.

Here are some notes I made after a day of messing with Haskell's package system.

Remember to include additional path directories for `haskell-ghc-mod`, which can include the following:

- `/Users/USERNAME/.local/bin`
- `/Users/USERNAME/Library/Haskell/bin`
- `/usr/local/bin`

# Creating a project in Stack

- `stack new {project name} simple` --Simple is the type of project
- `cd {project folder}`
- `stack setup`
- `stack build`

# Cabal

- `cabal init` --To start a new project (similar to package.json)
- `cabal update` --Get up to date packages
- `cabal install {package}` --Install dependencies for project
- `cabal build`

You can then use your project with `stack ghci`

# Checklist when something goes wrong

- Did you install GHC in your project folder
- Is GHC in your PATH
- Are your functions left justified
- Are IO functions on new line below `do`
- Check indentations

# More reading:

- [How I Start Haskell](http://howistart.org/posts/haskell/1)
- [Practical Haskell](http://seanhess.github.io/2015/08/04/practical-haskell-getting-started.html)
- [Haskell Atom Setup](https://github.com/simonmichael/haskell-atom-setup)
- [Configuring Your Haskell Environment](http://tonylawrence.com/2014/01/01/configuring-your-haskell-environment/)
