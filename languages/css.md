# CSS

## Flexbox

- Aims to replace the block model to provide predictable arrangement of elements on the screen across multiple screen sizes and devices
- Child elements can be laid out in any direction and have flexible dimensions to adapt to the display space.
  - the display order of the elements is independent of their order in the source code
- A flex container expands items to fill available free space, or shrinks them to prevent overflow
- The flexbox layout algorithm is direction-agnostic, it works well for pages but is best suited for components of the screen that change orientation, size and direction based on the user agent

### Usage

- `display: flex` - designate a block level flex container
- `display: inline-flex` - designate a inline level flex container

### Terminology

- **Flex container**: the parent element in which flex items are contained, defined by using the **flex** or **inline-flex** values of the **display** property
- **Flex item**: Each child of a flex container
- **Axes**: every flex layout follows two axes
  - **main axis** is the axis the flex items follow each other on
  - **cross axis** the axis perpendicular to the main axis
  - **flex-direction** establishes the main axis
  - **justify-content** how flex items are laid out along the main the axis on the current line
  - **align-items** defines the default for how flex items are laid out along the cross axis on the the current line
  - **align-self** defines how a singel flex item is aligned on the cross axis
  - **text-overflow** defines how overflowed text that is not displayed to the user is handled ie elluips
- **Directions**: the **main start** / **main end** and **cross start** / **cross end** sides of the flex container describe the origin and terminus of the flow of flex items, they follow
  the main axis and cross axis of the flex container in the vector established by the writing mode (left-to-right, right-to-left etc.)
  - **order**: assigns elements to the ordinal groups to determine which element appears first
  - **flex-flow** shorthands the **flex-direction** and **flex-wrap** properties to lay out flex items
- **Lines**: flex items can be laid out on either a single line or on several lines according to the **flex-wrap** property which controls the direction of the cross axis
  and the direction in which new lines are stacked
- **Dimensions**: the flex items' agnostic equuivalents of height and width are **main size** and **cross size**
  - the **min-height** and **min-width** properties default to 0
  - the **flex** property shorthands the **flex-grow**, **flex-shrink** and **flex-basis** properties

### Summary / interesting

- Still need to use autoprefixer at the moment
- A layout mode providing for the arrangement of element son a page
- Designed for layouts to be displayed at different sizes on different devices
- One of the key features is the ability to alter the width and height of items to best fill the available space
- it does not use floats and the margins collapse with margins of its contents
- text directly contained in a flex container is automatically wrapped in an anonymouse flex-item
- margins of adjacent flex items do not collapse
- Flexbox alignment is **true centering**, items will stay centered even if they overflow the container, if you dont want this behaviour use auto margins for centering
- use `break-after`, `break-before` and `break-inside` to control line breaks for a container, items or inside items

### Parent properties

- flex is a display property that is used for the container
  `.parent { display:flex; }`
  - if you dont define a height the items will stretch
- **flex-direction** controls the order the children elements are displayed in
  - **reverse-row**, **column**, **column-reverse** etc
- **flex-wrap** flex children won't take up more space than is dictated by the parent, flex-wrap dictates what should happen if their size is too big
  - the children will always appear on 1 line unless you specify
  - defaults to nowrap
- **justify-content** used to align the flex children
  - space-between: equally spaces the content within the full flex area
  - space-around: adds equal space left and right of every child
  - defaults to flex-start
- **align-items** used to align items vertically
  - stretch: takes up all the vertical space available
  - center: used to center
  - defaults to: flex-start
- **align-content** affects the vertical alignment of elements that are wrapped
  - the default is to stretch
  - applies to the content items when they are wrapped
  - **stretch**, **flex-end**, **space-around** ..etc

### Child properties

- **order**: Set the order the items should appear in
  - if you declare an order for an element it will become the first of all the items that have an order. unordered items will still appear first
  - if 2 elements have the same order, they will follow the order they are declared in the CSS
  - -ve numbers move to the front
- **flex-grow** control the ratio for how each element will grow
  - set to 1, gives even space to all the elements
  - set an element to 2, and it will grow with twice the size of the other elements
  - defaults to 0
- **flex-shrink** enables the element to shrink if there is not enough space within the container
- **flex-basis** Sets a starting point before the element will start to grow / shrink
  - depends on the direction of the flow (can affect the height / width depending on the direction)
- **align-self** allows you to change the alignment of the specific child
  - **flex-start**, **center**, **stretch** etc

## Modules

Allow us to interact with CSS definitions from inside javascript, a build script takes care of creating specific and unique names for each style and modifying the actual name in the style.

[More info](http://glenmaddern.com/articles/css-modules)

## PostCSS

## CSS Grid

- 2d system designed to handle columns and rows
- Rules are applied to a parent (Grid container) and children (Grid items)
- Works well in conjunction with flexbox which is largely based around 1 dimensional layouts
- Basic process
  - Define container with `display: grid`
  - Set the column and row sizes with `grid-template-column` and `grid-template-rows`
  - Add children with `grid-column` and `grid-row`
- The source order of the grid items does not matter

### Terms

- **Grid container**: Direct parent of all the grid items
- **Grid item**: Direct descendants of the grid container
- **Grid line**: The dividing line that makes up the structure of the grid
  - **Column grid lines**: Vertical lines
  - **Row grid lines**: Horizontal lines
- **Grid track**: Space between two adjacent grid lines, eg. the columns and rows of the grid
- **Grid cell**: The space between two adjacent row and two adjacent column grid lines, a single square of the grid
- **Grid area**: Total space surrounded by four grid lines
- **fr**: fraction of the free space, unit of measure
- **repeat()**: function used to repeat segments of grid template
- **minmax(minValue, maxValue)**: function to specify size bounds for a property
- **auto-fill**: create as many tracks as fit into the grid without causing it to overflow
  - `grid-template-columns: repeat(auto-fill, 100px);`
- **auto-fit**: same as auto-fill, except it will only create as many tracks as needed and will collapse any empty repeated tracks
  - `grid-template-columns: repeat(auto-fit, 100px);`
- **Explicit grids**: Manually defined number of lines and tracks using grid-template\* rules
- **Implicit grids**: When a grid item is placed outside of the explicit grid or there are more items than cells in the grid the grid container will automatically generate additional tracks. `grid-auto*` rules can be used to control the size of implicit tracks.

### Grid container properties

- **display**: defines the element as a grid container, creates a new grid formatting context for its content
  - values: grid, inline-grid
- **grid-template-(columns|rows)**: Defines the colums and rows of the grid with a space separated list of values.

```
.container {
  grid-template-columns: <track-size> <line-name> <track-size> <line-name>...
}

.container-with-named-tracks {
  // left edge is named first, then a 40px cell, line2, 50px cell and then the last line
  grid-template-columns: [first] 40px [line2] 50px [last];
  // First line has 2 labels, then a 100px high row, then then another line with 2 labels
  grid-template-rows: [top-row row1] 100px [bottom-row row2];
}

.container-with-repeated-sections {
  grid-template-columns: repeat(3, 20px [col-start]);
}
```

- track size: the size of each track (column or row) of the grid, the `fr` unit can be used to set the track to a fraction of the free space available, this is calculated after any non-flexible items
- line name: optional name for the given track-size, if omitted, tracks are given positive and negative numbers. If multiple lines share the same name, they can be referenced by their line name and count. Negative number start from the last line and work backwards

* **grid-template-areas**: Defines a grid template by referecing the names of the grid areas which are specified with the `grid-area` property.
  - Each row of the declaration needs to have the same numbe r of cells
  - In this way, you're only naming areas, not lines
  - Repeating the name of a grid area will span the content across the cells
  - A period signifies an empty cell
  - The syntax specifies the layout of the area

```

.item-a { grid-area: header; }
.item-b { grid-area: main; }
.item-c { grid-area: sidebar; }
.item-d { grid-area: footer; }

.container {
 // visually define the grid areas
 display: grid;
 grid-template-columns: repeat(4, 50px);
 grid-template-rows: auto;
 grid-template-areas:
  "header header header header"
  "main main . sidebar"
  "footer footer footer footer";
}
```

- **grid-template**: Shorthand for setting grid-template-(rows|columns|areas) in one
  - value: `none` resets all three properties
  - syntax: none | <grid-template-rows> / <grid-template-columns>
- **grid-(column|row)-gap**: Specifies the size of the grid lines, gutters between columns and rows
  - `grid-gap` can be used as a shorthand for both column and row settings
- **justify-items**: aligns grid items _inline_ along the row axis
  - takes similar values as the flexbox property
- **align-items**: Aligns grid items along the column axis, applies to all grid items inside the container
- **place-items**: sets both _align-items_ and _justify-items_
  - values: <align-items> / <justify-items>
- **grid-auto-(columns|rows)**: Specifies the size of any auto generated grid tracks aka _implicit tracks_
- **grid-auto-flow**: Specifies the placement of grid items that aren't explicitly placed on the grid
  - row: fill in each row in turn, adding new rows when needed
  - column: fill in each column in turn adding new columns when needed
  - dense: fill n holes earlier in the grid
- **grid**: Shorthand for specifiying a range of properties at once

### Grid items properties

- **grid-(column|row)-(start|end)**: Determine a grid items location with in the grid by referring to specific grid lines
  - grid-column-start / grid-row-start is the line where the item begins
  - grid-column-end / grid-row-end is where the item ends
  - values: number|name|span <number>|span <name>|auto
- **grid-(column|row)**: Shorthand for grid-(column|row)-(start|end)
  - values: start-line/end-line | start-line/span <value>
- **grid-area**: Gives an item a name so that it can be referenced by a template created with the `grid-template-areas` property, it can also be used as an even shorter shorthand for `grid-(column|row)`
  - values: name|row-start/column-start/row-end/column-end
- **(justify|align)-self**: Aligns a grid item inside a cell along the block or row axis
- **place-self**: Shorthand to specify both justify and align self

### Alignment values

- **justify-items|align-items|place-items**
  - start|end: align to be flush with the start|end edge of their cell
  - center: align items in the center of the cell
  - stretch: fill the whole width or height of the cell
- **justify-content|align-content|place-content**
  - start|center|end: aligns the grid to be flush with the start|end|center of the grid container
  - stretch: resize the grid items to allow the grid to fill the full width of the grid container
  - space-around: places an even amont of space between each grid item with half-size spaces on the far ends
  - space-between: places an even amount of space between each grid item wi th no space at the far ends
  - space-evenly: places an even amount of space betwene each grid item including the far ends

## Resources

- [MDN Flexible boxes](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Using_CSS_flexible_boxes)
- [MDN Flexbox for web applications](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Using_flexbox_to_lay_out_web_applications)
- [Good overview of the properties](https://www.youtube.com/watch?v=G7EIAgfkhmg)
- [CSS Tricks guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- [Scalable CSS](http://mrmrs.io/writing/2016/03/24/scalable-css/)
- [CSS-Tricks: A complete guide to grid](https://css-tricks.com/snippets/css/complete-guide-grid/)
- [MDN: CSS grid layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout)
- [Jen simmons - grid basics](https://www.youtube.com/watch?v=FEnRpy9Xfes)
