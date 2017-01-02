# d3.js
## General 

### set up a canvas using the svg element
`var canvas = d3.select("body")
                .append("svg")
                .attr("width", 700)
                .attr("height", 700);`
### set data for a selection
Creates a circle for each of the items in the data ... kinda
`var data = [10, 20, 30, 40];
 var canvas = d3.select('.container')
                .append("svg")
                ...
                .data(data)
                  .enter()
                  .append('circle')`
               
## Notes
* `.select(selector)` - select an element from the DOM for manipulation
* `.selectAll(selector)` - apply to all matching selectors
* `.append(selector)` - append the tag specified to the dom 
* `.text(text)` - write the text to the screen
* `.attr(name, value)` - set an attribute on the current element
  - when we are in a data set, the 2nd parameter is a function that takes an element from the data array in the form `function(datavalue, index)`
  - `.attr('transform')` - apply transformations such as translations, rotations etc
* `.data(source)` - specify the dataset for the selection
  - `.enter()` - start using the data we have selected
* `.scale()` - set the scaling used for the data
  - `.domain()` - min / max value
  - `.range()` - the size of the canvas that the domain is mapped to
* `.append('g')` - used to group items togethor, so they can be manipulated togethor
* `.axis()` - used to define axises for the visualisation
  - `ticks(number)` - the number of values to appear on the axis
  - use `.call()` to apply the axis to our canvas
* `d3.drag()` - creates a new drag behaviour, this returns an object and function that can be applied to selected elements with **selection.call**
  - `drag(selection)` - applies the behaviour to the specified selection
  - the behaviour can be unbound using `selection.on(".drag",null)`
  - `.on(typenames, listener)` - sets a listener for the drag event, such  as **start|drag|end**
    * **start**: after a new pointer becomes active (on mousedown or touchstart)
    * **drag**: after an active pointer moves (on mousemove or touchmove)
    * **end**: after a new pointer becomes inactive (on mouseup or touchend touchcancel)
  - `d3.event` is passed to the listener, with the fields
    * **target** - the associated drag behaviour
    * **type** - the type of event (start, drag, end)
    * **subject** - the drag subject
    * **x** - the new x co-ordinate of the subject
    * **y** - the new y co-ordinate of the subject
    * **dx** - the change in x co-ordinate since the last drag event
    * **dy** - the change in y co-ordinate since the last drag event
