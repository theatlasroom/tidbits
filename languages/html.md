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

### Methods
* `.closePath()` - automatically close a path
* `.fill(...)`
* `.stroke(...)`
* `.moveTo(x, y)` - moves the virtual cursor, for drawing on the screen
* `.lineTo(x, y)` - draws a line between the previous point (such as moveTo) and the specified x,y point
* `.rect(x,y,width,height)` - draw a rectangle
* `.fillRect(x,y,width,height)` - draws a rectangle at the parameters with the width / height specified and a fill colour
* `.strokeRect(x,y,width,height)` - draw a rectangle with a stroke outline
* `.clearRect(x,y,width,height)` - erase any content in the rectangle


### Events
