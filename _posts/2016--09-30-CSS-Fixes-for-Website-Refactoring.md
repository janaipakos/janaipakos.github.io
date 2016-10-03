---
layout: post
title: CSS Fixes for Website Refactoring
date: 2016-09-05
---
I found several surprises after running a pagespeed audit on this blog. The first was that  the site was not using 96% of Bootstrap's CSS. It has become second nature to import Bootstrap or Foundation while setting up a site, and I fell into this trap of going for simplicity instead of performance. The only Bootstrap code I was using was the grid system and navigation styling.

These were easy replacements after removing the Bootstrap CSS, thanks to flexbox. But while i was tinkering around, I started refactoring more and more CSS. Listed below are a few quick fixes that will improve CSS readability and squeeze performance from sites:

##PX, REM, EM
Em and rem are units of measurement translated into pixel values, and this flexibility helps them scale elements uniformly. Keith Grant uses a button with text as an example. With pixel units, resizing the interior text will not change the button size, and lead to janky looking elements. But with em referencing font-size, the button will scale.

Generally, rem should be used for font-size, em for padding/margins, and px for borders. Rem/em is preferred so that the element can size up and down accordingly to a point of reference, which could be the font-size of an element or, in the case of rem, the font-size made explicit in the root. Use the code below, then set your font to rem to set it relative to this!
```css
:root {
  font-size: 1em;
}
```
For the difference between rem and em, consider that nested elements will reference the previous element, rather than the root element. So a cascading list of nested unordered items will be smaller and smaller in size, for example, because they are each a smaller percentage in size of  the previous element. If unsure which unit to use, remember:
- Rem because font should scale, but also has to be relative to root because of the potential for nesting
- Em for the padding to scale
- Px because these measurements should be exact

##BEM Naming
Harry Roberts from [CSS Wizardry](http://csswizardry.com/) has more to say about this, but a quick note on the naming specification BEM that helped organize my CSS. BEM splits components’ classes into three groups, and it stands for:
- Block: The sole root of the component.
- Element: A component part of the Block.
- Modifier: A variant or extension of the Block.

An analogy is below. Here we can see that `.person {}` is the Block; it is the sole root of a discrete entity. `.person__head {}` is an Element; it is a smaller part of the `.person {}` Block. Finally, `.person--tall {}` is a Modifier; it is a specific variant of the `.person {} `Block.

- .person { }
- .person__head { }
- .person--tall { }

##Miscellaneous Fixes and References
- Use maxwidth instead of width for flexbility
- Add the property `hyphens` to text selectors for better readability. Only works on Firefox.
- Get rid of unused class names and unspecific class names. Think `post-title` instead of `title`. Remove overly specific class names such as `nav ul` and replace them with .site-nav
- Select what you want explicitly, rather than relying on circumstance or coincidence. Good Selector Intent will rein in the reach and leak of your styles.
- Write selectors for reusability, so that you can work more efficiently and reduce waste and repetition.
- Do not nest selectors unnecessarily, because this will increase specificity and affect where else you can use your styles.
- Do not qualify selectors unnecessarily, as this will impact the number of different elements you can apply styles to.
- Keep selectors as short as possible, in order to keep specificity down and performance up.
- Don't confuse your wording:
```css
[selector] {
  [property]: [value];
  [<--declaration--->]
}
```


## More Information
- [*CSS Secrets*](http://lea.verou.me/) by Lea Verdou
- [*CSS in Depth*](https://www.manning.com/books/css-in-depth) by Keith J. Grant