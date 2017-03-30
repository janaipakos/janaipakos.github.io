---
layout: post
title: Install Tidal for Stack
date: 2017-03-30
---

There is one small change necessary for running the [tidalcycles](https://tidalcycles.org/) plugin for Atom/VS.

- Install tidal as normal, set up Super Collider with `include("SuperDirt")` then `SuperDirt.Start`. 

- Install Atom or VS, then install the respective tidalcycles plugin. I did not need to change the default path to ghci from . . . `ghci`.

- Here is the difference: run your editor from within stack with `stack exec`. The windows command is in this [Reddit thread](https://www.reddit.com/r/haskell/comments/5nfiyi/how_to_completely_purge_my_computer_of_anything/dcc9y0x/), which this solution is from.

On Mac, this command is
```bash
stack exec /Applications/Atom.app/Contents/MacOS/Atom -- --processStart Atom.app
```

This will open a stacked instance of Atom, and then you can open your .tidal file and run the program (i.e. `d1 $ sound "bd cp"`) with `shift+enter`.