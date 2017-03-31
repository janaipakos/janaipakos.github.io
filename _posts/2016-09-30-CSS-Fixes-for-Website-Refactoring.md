---
layout: post
title: CSS Fixes for Website Refactoring
date: 2016-09-05
---
I found several surprises after running a pagespeed audit on this blog. The first was that  the site was not using 96% of Bootstrap's CSS. It has become second nature to import Bootstrap or Foundation while setting up a site, and I fell into this trap of going for simplicity instead of performance. The only Bootstrap code I was using was the grid system and navigation styling.

These were easy replacements after removing the Bootstrap CSS, thanks to flexbox. But while i was tinkering around, I started refactoring more and more CSS. Listed below are a few quick fixes that will improve CSS readability and squeeze performance from sites:

## PX, REM, EM
Em and rem are units of measurement translated into pixel values. An em is the font-size of the current element. This flexibility helps them scale elements uniformly. Keith Grant uses a button with text as an example. With pixel units, resizing the interior text will not change the button size, and lead to janky looking elements. But with em referencing font-size, the button will scale.

Generally, rem should be used for font-size, em for padding/margins/height/width/border-radius, and px for borders. Rem/em is preferred so that the element can size up and down accordingly to a point of reference, which could be the font-size of an element or, in the case of rem, the font-size made explicit in the root. 

Use the code below, then set your font to rem to set it relative to this!
```css
:root {
  font-size: 1em;
}
```

- The `html` element and `:root` are equivalent, with `:root` having a higher specificity.

For the difference between rem and em, consider that nested elements will reference the previous element, rather than the root element. So a cascading list of nested unordered items will be smaller and smaller in size, for example, because they are each a smaller percentage in size of  the previous element. This is the shrinking font problem, and it happens when each list item inherits the font-size of other items. If unsure which unit to use, remember:
- Rem because font should scale, but also has to be relative to root because of the potential for nesting
- Em for the padding to scale
- Px because these measurements should be exact

## BEM Naming
Harry Roberts from [CSS Wizardry](http://csswizardry.com/) has more to say about this, but a quick note on the naming specification BEM that helped organize my CSS. BEM splits components’ classes into three groups, and it stands for:
- Block: The sole root of the component.
- Element: A component part of the Block.
- Modifier: A variant or extension of the Block.

An analogy is below. Here we can see that `.person {}` is the Block; it is the sole root of a discrete entity. `.person__head {}` is an Element; it is a smaller part of the `.person {}` Block. Finally, `.person--tall {}` is a Modifier; it is a specific variant of the `.person {} `Block.

- .person { }
- .person__head { }
- .person--tall { }

## Miscellaneous Fixes and References
- Never use ids for selectors
- Never use !important
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

## Cascade Order
- LoVe HAte- link, visited, hover, active
- TRouBLe- Top, Right, Bottom, Left

## Viewport Units
The framed area in the browser window, in 1/100th or percent out of 100. For example, 50vh is 50% of the viewport height.
- vh: viewport height
- vw: viewport width
- vmin: the smaller dimension
- vmax: the larger dimension
- calc() combines measurements in different units i.e. `calc(1em + 16px)`

## Custom Properties
More powerful than variables in preprocessors. Useful for reocurring values such as color or font, as it only needs to be changed in one location.
- References by the function `var()` followed by the `--value` declared in the :root/html selector.
- Can be scoped to local property. Use `--value` as the property, and set a new value to overwrite the original. Not sure how this is better than just overwriting it with a normal property/value.

## Border Box
- Default property is `content-box`, which is the size set by the content. The padding, border, and magin is added after.
- `border-box` is prf s, where the height and width set the size of the content i.e. adding padding makes the content narrower (shrinks it to make room), rather than wider.
- Dont set a default column height. Use `min-height` or `max-height`. Use flex to sort out heights automatically.
- Vertical centering: give a container equal top and bottom padding, or use flexbox.
- The double container pattern is settling an inner container within an outer one in order to control the width of the page contents.
  - The body selector can serve as the outer container, with a `div class='container'` serving as the inner. 
  - One way to remember this is the idea of compiling React or PureScript code into a single div.
  - Set the max-width, and `margin: 0 auto` to restrain the inner container and center it.

## Flexbox

- `display: flex` turns an element into a flex conatiner, which makes its children (flex items) fill the width of the container.
- X axis is main axis, y axis is cross axis, listed left to right as start to end.
- The `flex` property resizes flex items width along the main axis
  - `flex` is shorthand for `flex-grow`, `flex-shrink`, and `flex-basis`
  - `flex-grow` is how much the item should grow to fill the remaining size left over from `basis`. This is proportionally based i.e. 2 is double the size of 1
  - `flex-shrink` how much should an item shrink. Can use percentage with just `flex` to signify this
  - `flex-basis` is the initial main size of the item in px, em, or percent
- `flex-direction` can take the value row, column, or the reverse to change the stack direction of flex items

## CSS Grid
- Grid layout that all browsers will support soon without prefixing.
- Define two-dimensional layout and then place elements within it.
- Set up with `display: grid`
  - property `grid-template-column/row` and the new value `1fr` (fraction unit), which is similar to `flex-grow`. Can use `repeat()` to define number and height. Can name the grid lines with [left] 1fr [center] 1fr [right]. Or name the grid areas with `grid-template-areas` to name the correct amount of rows and columns, then calling these names in the `grid-area` property.x
  - `grid-gap` is the amount of space between each cell
  - `grid-line` is horizontal or vertical structure of the grid
  - `grid-track` is space between grid line. Created with grid-template-col/row
  - `grid-cell` is a single place/cell where grid tracks intersect
  - `grid-area` is a rectangle of one or more grid cells
- Differences with flexbox: flex is one-dimensional, grid is two. You don't set size with flex, but grid has a size

## Always use

- Use the universal border-box fix, which targets every element and pseudo-element.

```css
:root {box-sizing: border-box;}
*, ::before,::after {box-sizing: inherit;}
```

## More Information

- [*CSS Secrets*](http://lea.verou.me/) by Lea Verou
- [*CSS in Depth*](https://www.manning.com/books/css-in-depth) by Keith J. Grant