# webgl

## Links

- [WebGL up and running]()

## General

Cross browser open source API that brings OpenGL ES 2.0 to the web as a 3D drawing context.
Uses the OpenGL shading language GLSL ES
ES - embedded systems, this version of OpenGL is targeted at mobile devices and works well for a web context.
Webgl uses the existing **canvas** object in the browser, but uses a special drawing context

Basic terminologies and concepts

- **mesh** - an object composed of one or more polygonal shapes, constructed from vertices that define the coordinate positions in 3D space
  - defined by the positions of their vertices
  - triangles are the most common type of polygons and quads
  - surface attributes define how the look of the mesh, such as how light reflects off the object, how shiy objects look
- `texture map (textures)` - bitmaps that define the surface look for a mesh
  - can be combined togethor to give complex effects such as bumpiness or iridescence
- **materials** - collective term for the surface properties of a mesh
  - rely on the presence of one or more lights which define how a scene is illuminated
- **model** - 3D mesh
- **transforms** - operations that move a mesh by a relative amount, explicity changing its position
  - allow a mesh to be translated, scaled or rotated without changing any values in its vertices
  - represented by matrices
- **matrix** - a mathematical objecvt containing an array of values to compute the transformed vertex positions
  - **ModelView** - matrix used to define the position of a mesh relative to the camera
  - **ProjectionMatrix** - required by the shader to convert the 3D coords of the model in camera space, into the 2D viewport space
- **camera** - an object that defines where the user is **positioned** and **oriented** relative to the scene
  - **field of view** - defines the perspective (objects further away appear smaller)
  - the cameras properties combine to render a 3D scene into a 2D viewport defined by the window / canvas
  - **projection matrix** - defines the translation of 3D coordinates into the 2D viewport
  - **clipping planes** - the **near** and **far** planes define the boundaries of a subset of the 3D space (view frustrum)
  - **view frustrum** - objects appearing in this area are the only ones actually rendered to the screen
- **shaders** - a chunk of code that defiens how vertices, transforms, materials, lights and the camera all interact
  - the shading process provides 3 dimensionality to our objects
  - programs written in a high-level C-like language to get the pixels for a mesh onto the screen
  - shaders are compiled into code that is usable by the GPU
  - WebGL requires a shader before anything can be rendered
  - a shader needs to be provided for each object that is rendered
  - **vertex shader** - transforms the coordinates of the object into 2D space
  - **fragment shader** - generate a final colour for each pixel in the transformed vertices, based on the color, texture, lighting and material inputs
- **lights** - sources of light for our scene
  - use the **.position** attribute of the light to set its location relative to the origin, direction is then inferred to point _into_ the origin of the scene
  - **directional** - illuminates objects from a specific direction, but over a infinite distance and doesnt have a particular location

To render a WebGL scene we need to:

1. Create a canvas

- all WebGL rendering takes place in a **context**, a JS DOM object that provides the complete WebGL API

2. Obtain a drawing context for the canvas

- create a **canvas** tag on the page and get a reference to the context from the context

3. Initialize the viewport

- Give boundaries to the context that you have retrieved, this is the viewport
- Call the context's viewport() method

4. Create one or more buffers containing the data to be rendered (such as vertices)
5. Create one or more matrices to define the transformation from vertex buffers to the screen
6. Create one or more shaders to implement the drawing algorithm we want
7. Initialize the shaders with the parameters we want
8. Draw

## Data types

- **ArrayBuffer** - typed arrays for storing compact binary data, they can be accessed by javascript using normal array syntax
- **Float32Array** - a type of ArrayBuffer

## Primitives

WebGL drawing is done with primitives, these primitives use arrays of data (buffers) which define the positions of the vertices to be drawn.

- **triangle sets**
- **triangle strips**
- **points**
- **lines**

## GL Context

- `.viewport(start, end, width, height)` - set the boundaries of our context
- `.bindBuffer`
- `.bufferData`

### Constants

- `.ARRAY_BUFFER`
- `.STATIC_DRAW`
- `.TRIANGLE_STRIPC`

[//]: Might have to move these to seperate files?

## Threejs

A library that abstracts the details of the WebGL API, representing the 3D scene as meshes, materials and lights

- **renderer** - responsible for all drawing, it uses a WebGL context under the hood
  - the renderer object should be constructed and added to the DOM
  - **render** - takes a scene and a camera and renders to the screen
  - `.domElement` - returns the dom mode for us to add to our page
- **scene** - top level object that contains all the other graphical objects
  - in Threejs objects exist in a parent-child hierarchy
- **camera** - defines where we are viewing the scene from
  - position.set(x,y,z) to move the camera
- **meshes**
  - **PlaneGeometry** - constructs a rectangle, taking width and height as parameters
  - **CubeGeometry** - create cubes
- **materials**
  - **MeshBasicMaterial** - creates a simple material with the colour white

[//]: Might have to move these to seperate files?

## GLSL

- [Madebyevan](http://madebyevan.com/)
