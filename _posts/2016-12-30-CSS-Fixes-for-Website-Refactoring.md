---
layout: post
title: CSS Fixes for Website Refactoring
date: 2016-12-30
---
After running a pagespeed audit, I found that this site uses 10% of Bootstrap's CSS. It's second nature to import Bootstrap or Foundation while setting up a site, and I fell into this trap of going for simplicity instead of performance.

While I was tinkering around, I started refactoring more and more CSS. Listed below are references and fixes that will improve CSS readability and maintainability, and squeeze performance from sites:

## PX, REM, EM

- Em and rem are units of measurement translated into pixel values. An em is the font-size of the current element, and it helps the element scale uniformly. For example, a button with text. With pixel units, resizing the interior text will not change the button size. But with em referencing font-size, the button will scale.

- Use the code below, then set your font to rem to set it relative to this!

```css
:root {
  font-size: 1em;
}
```

- The `html` element and `:root` are the same, but `:root` has a higher specificity.

- For the difference between rem and em, consider that nested elements will reference the previous element, rather than the root element. For example, a cascading list of nested unordered items will be smaller and smaller in size, because they are each a smaller percentage in size of the previous element. This is the shrinking font problem, and it happens when each list item inherits the font-size of other items. If unsure which unit to use, remember:
  - Rem in `font-size` so it can scale and also be relative to root because of the potential for nesting
  - Em in padding/margins/height/width/border-radius
  - Rem/em lets elements size uniformly accordingly to a point of reference, which could be the font-size of an element or the font-size made explicit in the root.
  - Px for borders because these measurements should be exact

## BEM Naming
Harry Roberts from [CSS Wizardry](http://csswizardry.com/) mentions the naming specification called BEM. BEM splits components’ classes into three groups, and it stands for:
- Block: The sole root of the component.
- Element: A component part of the Block.
- Modifier: A variant or extension of the Block.

An analogy is below. Here we can see that `.person {}` is the Block; it's the sole root of a discrete entity. `.person__head {}` is an Element; it's a smaller part of the `.person {}` Block. `.person--tall {}` is a Modifier; it's a specific variant of the `.person {}` Block.

- .person { }
- .person__head { }
- .person--tall { }

## Miscellaneous Fixes and References
- Never use ids for selectors. This screws with specificity
- Never use !important
- Use maxwidth instead of width for flexbility
- Add the property `hyphens` to text selectors for better readability
- Get rid of unused class names and unspecific class names. Think `post-title` instead of `title`. Remove overly generic class names such as `nav ul` and replace them with `.site-nav`
- Select what you want explicitly, rather than relying on circumstance or coincidence. Good Selector Intent will rein in the reach and leak of your styles
- Write selectors for reusability, so that you can work more efficiently and reduce waste and repetition
- Do not nest selectors unnecessarily, because this will increase specificity and affect where else you can use your styles
- Do not qualify selectors unnecessarily, as this will impact the number of different elements you can apply styles to
- Keep selectors as short as possible to keep specificity down and performance up
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

More powerful than variables in preprocessors. Useful for reoccurring values such as color or font with one location of change.
- References by the function `var()` followed by the `--value` declared in the :root/html selector
- Can scope to local property. Use `--value` as the property, and set a new value to overwrite the original

## Border Box

- Default property is `content-box`, which is the size set by the content. The padding, border, and margin is added after
- `border-box`, the height and width set the size of the content i.e. adding padding makes the content narrower (shrinks it to make room), rather than wider
- Don't set a default column height. Use `min-height` or `max-height`. Use flex to sort out heights automatically
- Vertical centering: give a container equal top and bottom padding, or use flexbox
- The double container pattern is setting an inner container within an outer container to control the width of the page contents.
  - The body selector can serve as the outer container, with a `div class='container'` serving as the inner.
  - One way to remember this is the idea of compiling React or PureScript code into a single div.
  - Set the max-width, and `margin: 0 auto` to restrain the inner container and center it.

## Flexbox

- `display: flex` turns an element into a flex container, which makes its children (flex items) fill the width of the container.
- X axis is main axis, Y axis is cross axis, listed left to right as start to end.
- The `flex` property resizes flex items width along the main axis
  - `flex` is shorthand for `flex-grow`, `flex-shrink`, and `flex-basis`
  - `flex-grow` is how much the item should grow to fill the remaining size left over from `basis`. This is proportionally based i.e. 2 is double the size of 1
  - `flex-shrink` how much should an item shrink. Can use percentage with `flex` to signify this
  - `flex-basis` is the initial main size of the item in px, em, or percent
- `flex-direction` can take the value row, column, or the reverse to change the stack direction of flex items

## CSS Grid

- Grid layout that all browsers will support soon without prefixing.
- Define two-dimensional layout and then place elements within it.
- Set up with `display: grid`
  - property `grid-template-column/row` and the new value `1fr` (fraction unit), which is similar to `flex-grow`. Can use `repeat()` to define number and height. Can name the grid lines with [left] 1fr [center] 1fr [right]. Or name the grid areas with `grid-template-areas` to name the correct amount of rows and columns, then calling these names in the `grid-area` property.
  - `grid-gap` is the amount of space between each cell
  - `grid-line` is horizontal or vertical structure of the grid
  - `grid-track` is space between grid line. Created with grid-template-col/row
  - `grid-cell` is a single place/cell where grid tracks intersect
  - `grid-area` is a rectangle of one or more grid cells
  - `grid-auto-flow` is the order of item placement. Value of row or column and an optional word `dense` to attempt and fill gaps
- Differences with flexbox: flex is one-dimensional, grid is two. You don't set size with flex, but grid has a size

## More Information

- [*CSS Secrets*](http://lea.verou.me/) by Lea Verou
- [*CSS in Depth*](https://www.manning.com/books/css-in-depth) by Keith J. Grant
