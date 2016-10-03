---
layout: post
title: Setting Up a Haskell Project
date: 2016-08-07
---

I haven't found the perfect Haskell IDE yet. Atom and Sublime both have alright plugin support and linting. Testing is done through `hlint` and there is GHC support in both. Unfortunately, I have had bad luck getting `stylish-haskell` to run in either. Nevertheless, Atom is my preferred, through its packages `language-haskell`, `ide-haskell`, and `haskell-ghc-mod`. Outside of these two, vim is another good option.

Here are some notes I made after a day of messing with Haskell's package system.

# Creating a project in Stack
## Download
- Download Stack from [Haskell Stack](https://haskell-lang.org/get-started)
- Can also use `brew install haskell-stack`

## Scaffold
- Create a new project, simply by writing one in a single file or using `stack new {project-name}`. This does a bit of scaffolding with folders, files, etc. You can also use a few [different templates](https://github.com/commercialhaskell/stack-templates) that set up the project in different ways.
- Something I learned from Christopher Allen's [_Haskell Mega Stack Tutorial_](https://www.youtube.com/watch?v=sRonIB8ZStw) is that Stack and Cabal are not package managers! GHC-PKG is the package manager.
- `cd {project folder}`
- Use `stack setup` to download and configure ghci using resolvers after switching to the new directory. Resolver or snapshots are all the same thing. These are just different updates or builds used to install ghc.
- `stack build` wil compile the project
- Run the compiled output or file with `stack ghci` or `stack build` and `stack exec {project-name}`.

##PATH
If you want to add ghci and ghc to your PATH, you could export it directly in the Terminal, but this will only be for that temporary session. A better solution is, on Mac, changing your PATH through `$HOME/.bash_profile` or by creating a file with paths in `/etc/paths.d`. In `$HOME/.bash_profile`, just type `export PATH=$HOME/{PATH HERE}:$PATH`.

Now you can call GHCI from the Terminal/bash.

# Installing libraries and CLI with stack

For importing dependencies and libraries, use `stack build {library}`. This will make a copy of the library that can be used across snapshots. Pretty nice. You can also add these to your stack.yaml in the project directory under 'extra-deps'. However, for CLI, such as Pandoc, use `stack install {CLI}`.

# PATH directories

Remember to include additional path directories for `haskell-ghc-mod`, which can include the following:

- `/Users/USERNAME/.local/bin`
- `/$HOME/Library/Haskell/bin`
- `/usr/local/bin`

# Deprecated Cabal Install

- Cabal is included in Stack, so the below steps are unnecessary. However, you may still need to edit the cabal metadata file that includes project description and dependencies.
- `cabal init` --To start a new project (similar to package.json)
- `cabal update` --Get up to date packages
- `cabal install {package}` --Install dependencies for project
- `cabal build`

# Checklist when something goes wrong

- Did you install GHC in your project folder
- Is stack and GHC in your PATH
- Are your functions left justified
- Are IO functions on new line below `do`
- Check indentations

# More reading:

- [How I Start Haskell](http://howistart.org/posts/haskell/1)
- [Practical Haskell](http://seanhess.github.io/2015/08/04/practical-haskell-getting-started.html)
- [Haskell Atom Setup](https://github.com/simonmichael/haskell-atom-setup)
- [Configuring Your Haskell Environment](http://tonylawrence.com/2014/01/01/configuring-your-haskell-environment/)
- [Haskell Stack Docs](https://docs.haskellstack.org/en/stable/install_and_upgrade/)
