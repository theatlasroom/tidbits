# HTML(5)?
## Media
### Video
`<video>`

### Events
audio and video elements trigger various events along the way.
* **abort** - sent when playback is aborted, ie the media is playing and playback is restarted from the beginning
* **canplay** - sent when enough data is available that the media can be played at least for a few frames
* **canplaythrough** - when the entire media can be played without interruption assuming the download rate remains at least at its current level
  - also fires when playback toggles from paused to playing
* **durationchange** - the metadata has loaded or changed, indicating a change in the duration of the media, ie when enough has loaded to show the duration
* **emptied** - the media has become empty, ie if it was partially loaded and the `load()` event is called to reload it
* **ended** - playback has completed
* **error** - an error has occurred
* **loadeddata** - the first frame of the media has finished loading
* **loadedmetadata** - all metadata has finished loading
* **loadstart** - loading has started
* **pause** - playback is paused
* **play** - playback is started after having been previously paused
* **playing** - the media begins to play
  - for the first time
  - after being paused
  - after finishing and automatically restarting
* **progress** - shows progress of the download
  - the amount downloaded so far is available in the media elements **buffered** attribute
* **ratechange** - playback speed change
* **seeked** - seek operation has completed
* **seeking** - seek operation has begun
* **stalled** - data unexpectadly not loading
* **suspend** - download has completed or is paused
* **timeupdate** - the elements **currentTime** attribute has changed
* **volumechanged** - the audio volume has changed
  - also sent when the muted attribute is changed
* **waiting** - the selected operation is delayed pending the completion of another event

## Canvas
`<canvas>`
* defaults to width 300 and height 150
* dont use css to set the size of the canvas, css will only set the layout size so the content will be stretch / scaled to fit the canvas dimensions
* you can set the width / height of the canvas by first getting the DOM element then setting the height / width manually
  ```
  const canvas = document.createElement('canvas');
  document.body.appendChild(canvas);
  canvas.width = 1080;
  canvas.height = 568;
  ```
* the context allows you to manipulate the canvas
  ```
  canvas.getContext("2d")
  ```
* paths - series of points with lines / curves between them
  ```
  context.beginPath();
  // draw commands
  context.fill(...); // or context.stroke(...)
  ```
* gradients can be created to fill a path with a range of colours
  ```
  let gradient =  context.createLinearGradient(100, 100, 200, 200);
  gradient.addColorStop(0, "red");
  gradient.addColorStop(0.5, "green");
  gradient.addColorStop(1, "blue");
  context.fillStyle = gradient;
  context.fillRect(0, 100, 100, 100);
  ```

### Methods
* `.closePath()` - automatically close a path
* `.fill()` - draw a fill for the shape
* `.stroke()` - draw a strokes for the shape
* `.strokeStyle` - sets the colour for the strokes, takes rgb, rgba, hex, css colour values
* `.fillStyle` - sets the fill colour, takes rgb, rgba, hex, css colour values | can be set to **gradient** for a gradient
* `.lineWidth` - set the width of the stroke
* `.lineCap` - sets the shape of the endpoint of a path, but not corners that join other lines, can be: but | round | square
* `.lineJoin` - shape the point where 2 lines join can be: miter | round | bevel
* `.moveTo(x, y)` - moves the virtual cursor, for drawing on the screen
* `.lineTo(x, y)` - draws a line between the previous point (such as moveTo) and the specified x,y point
* `.rect(x,y,width,height)` - draw a rectangle
* `.fillRect(x,y,width,height)` - draws a rectangle at the parameters with the width / height specified and a fill colour
* `.strokeRect(x,y,width,height)` - draw a rectangle with a stroke outline
* `.clearRect(x,y,width,height)` - erase any content in the rectangle
* `.quadraticCurveTo(cx, cy, x, y)` - draws a curve from the current point to the target point, the control point (cx, cy) is used to control the curvature
* `.bezierCurveTo(cx1, cy1, cx2, cy2, x, y)` - draws a curve using 2 control points
* `.arc(x,y,radius,startAngle,endAngle,antiClockwise)` - draw a circle or segments of a circle,
  - x,y specify the centre point of the circle
  - radius is the radius of the circle
  - startAngle / endAngle specify how far the arc should go around the circumference, ie 0 -> pi would draw a semicircle
  - antiClockwise defaults to false, so the circle will be drawn clockwise by default
* `.createLinearGradient(x1, y1, x2, y2)` - sets up a linear gradient
* `.createRadialGradient(x1, y1, radius1, x2, y2, radius2)` - sets a radial gradient
* `.addColorStop(position, color)` - adds a colour to the gradient, position specifies where this colour will start (value between 0 and 1)

### Events
