# CSS
## Flexbox
* Still need to use autoprefixer at the moment
* A layout mode providing for the arrangement of element son a page
* Designed for layouts to be displayed at different sizes on different devices
* it does not use floats and the margins collapse with margins of its contents

### Parent properties
* flex is a display property that is used for the container
  `.parent { display:flex; }`
  - if you dont define a height the items will stretch
* flex-direction: controls the order the children elements are displayed in
  - `reverse-row`, `column`, `column-reverse` etc
* flex-wrap: flex children won't take up more space than is dictated by the parent, flex-wrap dictates what should happen if their size is too big
  - the children will always appear on 1 line unless you specify
  - defaults to nowrap
* justify-content: used to align the flex children
  - space-between: equally spaces the content within the full flex area
  - space-around: adds equal space left and right of every child
  - defaults to flex-start
* align-items: used to align items vertically
  - stretch: takes up all the vertical space available
  - center: used to center
  - defaults to: flex-start
* align-content: affects the vertical alignment of elements that are wrapped
  - the default is to stretch
  - applies to the content items when they are wrapped
  - `stretch`, `flex-end`, `space-around` ..etc

### Child properties
* order: Set the order the items should appear in
  - if you declare an order for an element it will become the first of all the items that have an order. unordered items will still appear first
  - if 2 elements have the same order, they will follow the order they are declared in the CSS
  - -ve numbers move to the front
* flex-grow: control the ratio for how each element will grow
  - set to 1, gives even space to all the elements
  - set an element to 2, and it will grow with twice the size of the other elements
  - defaults to 0  
* flex-shrink: enables the element to shrink if there is not enough space within the container
* flex-basis: Sets a starting point before the element will start to grow / shrink
  - depends on the direction of the flow (can affect the height / width depending on the direction)
* align-self: allows you to change the alignment of the specific child
  - `flex-start`, `center`, `stretch` etc

## Resources
* [MDN Flexible boxes](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Using_CSS_flexible_boxes)
* [Good overview of the properties](https://www.youtube.com/watch?v=G7EIAgfkhmg)
* [CSS Tricks guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
