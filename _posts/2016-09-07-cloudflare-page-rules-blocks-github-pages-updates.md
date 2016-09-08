---
layout: post
title: Cloudflare Page Rules Blocks GitHub Pages Updates
date: 2016-09-07
---
A warning to users looking for faster page speeds. Cloudflare's Page Rule `Browser Cache TTL` will ignore any new pushes to GitHub Pages until the time period passes. This can be a few hours up until a month. Workarounds include:

- Cache only static pages and not the Blog
- Lower the Brwser Cache time period to a few hours
- Turn off Browser Caching

As a note to my future self, next time you are trying to see if a new Jekyll update broke the build, check Cloudflare's settings first.
