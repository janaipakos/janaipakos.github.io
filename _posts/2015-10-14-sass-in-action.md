---
layout: post
title: Sass in Action
date: 2015-10-14
---

I've been working with Sass for the past few months and wanted to post a few resources that I've come across.


Part of the reason for this post is the UI designer of five years who told me he does not use a preprocessor. My heart goes out to him.

## Benefits of Preprocessors


To start with, why use a preprocessor? Mainly because they will keep the developer sane while producing clean and maintanable CSS. Two of the most popular CSS frameworks are Sass and LESS. I prefer Sass because it has Compass.


Compass is a Sass framework designed to make styling smooth and efficient. Similar to Express acting as a framework for web applications with Node.js, with packages pulled from npm, Compass is a way to find reusable modules and snippets for Sass.

Here are some of the perks of preprocessors, which are 95% similar, and I'll list the differences next.


Variables (`$variable: #value`) allow you to organize property values at the top of your stylesheet, so there is no more hunting or command-F'ing for a hex value. These are declared like CSS properties, with any value able to be used with a variable. A variable's scope can be gobal as well as blocked. These can also be used in mixins, which let you resuse chunks of styles and plug in arguments.


One of the huge benefits of Sass is its ability to import other stylesheets without a performance hit. The `@import` rule lets one CSS file bring in the rules from another. Traditionally, the browser had to download these CSS files, which made importing less practical than just including all the rules in one file. What sets Sass apart when importing is that files are brought in when compiling to CSS, which means nothing extra is downloaded. In other words, more modular stylesheets.


Everyone has a different naming convention for their markup--find one that your group agrees on.


## Differences in Sass and SCSS


A few notes on the difference between Sass and the SCSS syntax, which stands for Sassy CSS. SCSS is a superset of CSS, meaning that any valid CSS file is also a valid SCSS file. So the CSS file `style.css` can be changed to `style.scss` and you can make Sass changes without a hitch. I prefer the SCSS syntax to Sass.


Here are a few of the differences. Sass uses an indented syntax that uses newlines to separate properties. Sass proponents like the clean look of their markup without semicolons and curly braces, and SCSS users like the ability to have whitespace wherever, or to have the ability to write one long line.


Mixins differ as well. SCSS uses `@mixin` and `@include` and while Sass can use these directives in the same way, it can also replace `=` and `+` for the directives, respectively. Again this is seen as cleaner code, but at the sake of clarity.


Comments in Sass only require one marker, such as `//`, `/*`, and `/*!`, even if the comment is multi-line. In SCSS, `//` marks a single-line comment, and must appear on each new lines.


Both syntaxes have their pros and cons. Luckily the two syntaxes are convertable with the `sass-convert` command, and the `@import` directive allows you to use each syntax in the same project, as long as they are in different files.


To close this out, here are some ways to straighten out your CSS and get started with Sass. These are found in [*Sass and Compass in Action*](https://www.manning.com/books/sass-and-compass-in-action) (Wynn Netherland, Nathan Weizenbaum, Chris Eppstein, Brandon Mathis, 2013), which also lists Compass traits for a fresh project.


- Grid-background, global reset, typography from [Google Font](https://www.google.com/fonts "Google Fonts"), [Font Squirrel](https://fontsquirrel.com "Font Squirrel"), and [Makerbook](https://makerbook.net "Makerbook")
- CSS3 Mixins: border-radius, text-shadow, box-shadow, gradients, spriting, vendor-prefixes
- Dust-me-selector, which removes unused CSS
- Serve and Middleman, which helps build static websites, built on Rails
- Client-side performance: [YSlow](http://developer.yahoo.com/yslow "YSlow"), [Google PageSpeed](http://developers.google.com/speed/pagespeed "Google PageSpeed"), and [WebPagetest](http://www.webpagetest.org)
