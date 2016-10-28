# CSS
## Flexbox
* Aims to replace the block model to provide predictable arrangement of elements on the screen across multiple screen sizes and devices
* Child elements can be laid out in any direction and have flexible dimensions to adapt to the display space.
  - the display order of the elements is independent of their order in the source code
* A flex container expands items to fill available free space, or shrinks them to prevent overflow
* The flexbox layout algorithm is direction-agnostic, it works well for pages but is best suited for components of the screen that change orientation, size and direction based on the user agent

### Usage


### Terminology
* **Flex container**: the parent element in which flex items are contained, defined by using the **flex** or **inline-flex** values of the **display** property
* **Flex item**: Each child of a flex container
* **Axes**: every flex layout follows two axes
  - **main axis** is the axis the flex items follow each other on
  - **cross axis** the axis perpendicular to the main axis
  - **flex-direction** establishes the main axis
  - **justify-content** how flex items are laid out along the main the axis on the current line
  - **align-items** defines the default for how flex items are laid out along the cross axis on the the current line
  - **align-self** defines how a singel flex item is aligned on the cross axis
* **Directions**: the **main start** / **main end** and **cross start** / **cross end** sides of the flex container describe the origin and terminus of the flow of flex items, they follow
  the main axis and cross axis of the flex container in the vector established by the writing mode (left-to-right, right-to-left etc.)
  - **order**: assigns elements to the ordinal groups to determine which element appears first
  - **flex-flow** shorthands the **flex-direction** and **flex-wrap** properties to lay out flex items
* **Lines**: flex items can be laid out on either a single line or on several lines according to the **flex-wrap** property which controls the direction of the cross axis
  and the direction in which new lines are stacked
* **Dimensions**: the flex items' agnostic equuivalents of height and width are **main size** and **cross size**
  - the **min-height** and **min-width** properties default to 0
  - the **flex** property shorthands the **flex-grow**, **flex-shrink** and **flex-basis** properties

### Summary
* Still need to use autoprefixer at the moment
* A layout mode providing for the arrangement of element son a page
* Designed for layouts to be displayed at different sizes on different devices
* One of the key features is the ability to alter the width and height of items to best fill the available space
* it does not use floats and the margins collapse with margins of its contents

### Parent properties
* flex is a display property that is used for the container
  `.parent { display:flex; }`
  - if you dont define a height the items will stretch
* **flex-direction** controls the order the children elements are displayed in
  - **reverse-row**, **column**, **column-reverse** etc
* **flex-wrap** flex children won't take up more space than is dictated by the parent, flex-wrap dictates what should happen if their size is too big
  - the children will always appear on 1 line unless you specify
  - defaults to nowrap
* **justify-content** used to align the flex children
  - space-between: equally spaces the content within the full flex area
  - space-around: adds equal space left and right of every child
  - defaults to flex-start
* **align-items** used to align items vertically
  - stretch: takes up all the vertical space available
  - center: used to center
  - defaults to: flex-start
* **align-content** affects the vertical alignment of elements that are wrapped
  - the default is to stretch
  - applies to the content items when they are wrapped
  - **stretch**, **flex-end**, **space-around** ..etc

### Child properties
* **order**: Set the order the items should appear in
  - if you declare an order for an element it will become the first of all the items that have an order. unordered items will still appear first
  - if 2 elements have the same order, they will follow the order they are declared in the CSS
  - -ve numbers move to the front
* **flex-grow** control the ratio for how each element will grow
  - set to 1, gives even space to all the elements
  - set an element to 2, and it will grow with twice the size of the other elements
  - defaults to 0  
* **flex-shrink** enables the element to shrink if there is not enough space within the container
* **flex-basis** Sets a starting point before the element will start to grow / shrink
  - depends on the direction of the flow (can affect the height / width depending on the direction)
* **align-self** allows you to change the alignment of the specific child
  - **flex-start**, **center**, **stretch** etc

## Modules
Allow us to interact with CSS definitions from inside javascript, a build script takes care of creating specific and unique names for each style and modifying the actual name in the style.

[More info](http://glenmaddern.com/articles/css-modules)

## PostCSS


## Resources
* [MDN Flexible boxes](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Using_CSS_flexible_boxes)
* [Good overview of the properties](https://www.youtube.com/watch?v=G7EIAgfkhmg)
* [CSS Tricks guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
