# Aframe
[A-Frame](https://aframe.io)
- Open source frameowrk for 3d and VR content built on three.js
- Built by MozVR team for prototyping WebVR content
- Easily create multiplatform VR scenes for desktop, Oculus rift and mobile
- Based on the `entity-component-system pattern (ECS)`, focused on composability over inheritance
  * **entity**: a general purpose object that does and renders nothing
      - Represented via an HTML element ie `<a-entity>`
  * **component**: a resuable module that is plugged into entities to provide appearance, behaviour and/or functionality
      - represented via a html attribute
      - component properties are represented by values defined in a attribute
  * **system**: provides global scope, services and management for components
  * Lets us build complex entities with rich behaviour by plugging different reusable components into the sockets on the entity

## General
* uses a right hand coordinate system (x right, y up, z out of the screen)
* the basic distance unit is in meters
* rotations are defined in degrees
* transformations (translation, rotation and scaling) are applied as components
   - `<a-scene>
        <a-box color="#6173F4" width="4" height="10" depth="2"
               position="-10 2 5" rotation="0 0 45" scale="2 0.5 3"></a-box>
      </a-scene>`
* use the src attribute to apply a texture (image or video)
  - it is best to cache the texture and block the scene from rendering until the texture has loaded.

## Entities
Represented by the `<a-entity>` element, they are placeholder objects which we plug components in, to provide them with appearance, behaviour and functionality.
Attached with the position, rotation and scale components
Entities can be retrieved using DOM APIs
`<a-entity>.components` - an object of components attached to the entity, gives access to all the entity components, their data methods and API

* `<a-animation>` - animates an entity
* `<a-assets>` -
  - useful for caching assets that are needed within the scene, ie images.
  - define the asset in the entity and give the asset an id, refer to the asset using the id selector `#asset`
* `<a-camera>` - used to explicitly define a camera, if it is not there then the default camera is used
* `<a-cursor>` - used to interact with entities
* `<a-image>` - Load an image and display it on a 2d plane
* `<a-light>` - change how the scene is lit
  - by default and ambient light and directional light will be added
  - once we add our own lights, the default is removed
* `<a-mixin>` - used to compose and reuse commonly-used sets of component properties
  - should be defined within a `<a-assets>`
  - `<a-scene>
      <a-assets>
        <a-mixin id="red" material="color: red"></a--mixin>
      </a-assets>
      <a-entity mixin="red cube"></a-entity>
     </a-scene>`
  - mixins are applied in the order they are defined, the last definition of a property will overwrite previous definitions
* `<a-sky>` - add a background to the scene, can be a color, video, image 360 degree assets etc
* `<a-video>` - displays a video on a flat plane as a texture,

## Components
Reusable and modular chink of data, plugged into an entity to add behaviour, functionality, appearance etc
All components have property types
* **Stats** - displays a UI with performance related metrics, applies only to the `<a-scene>` element
  - `<a-scene stats></a-scene>`
  - **fps**
  - **raf latency** - requestAnimationFrame
  - **Textures** - threejs textures
  - **Programs** - number GLSL shaders in the scene
  - **Geometries**
  - **Vertices**
  - **Faces**
  - **Calls** - number of draw calls on each frame
  - **Load time** - how long it took for the scene to start rendering in ms
  - **Entities** - number of A-frame entities
* **Material** - gives appearance to an entity, often paired with a geometry object which provides shape
  - **depthTest** - whether depth testing is enabled when rendering the material
  - **flatShading** - Use THREE.FlatShading rather than THREE.StandardShading
  - **opacity** - extent of transparency, if the transparent property is not true then the material willbe opaque and opacity will only affect the colour
  - **transparent** - whether material is transparent, transparent entities are rendered after non-transparent ones
  - **shader** - which material to use, defaults to standard material, but can be a registered custom material
  - **side** - which sides of the mesh to render, front, back or double
  - **materialtextureloaded** - event fired when the texture is loaded onto the material, or the first frame of video is playing
  - **materialvideoended** - for video textures when the video has reached its not (might not work for loop)
  - **standard material** - the default material, uses THREE.MeshStandardMaterial and has properties like **color**, **height**, **fog**, **metalness**, **repeat**, **roughness**, **width**, **src** (can be a url or selector for an img/video)

## System
Provides global scope, services and management to classes of components, provides public apis for classes to components.
Can be accessed through the scene element and can help components interface with the global scene
ie - the camera system manages all entities with the camera component, controlling which is the active camerai
- Register a system similar to a component using `AFRAME.registerSystem('name', {})`
- contains a **schema** and **data** (data provided by the schema available across handlers and methods) property 
- systems are accessed through the scene `document.querySelector('scene').systems[systemName]`

## Scene
The global root object, all entities are enclosed within the scene
The scene inherits from the Entity class, including the ability to attach components and the behavior to wait for all of its child nodes (assets, entities) to load before rendering
- setup canvas, renderer and render loop
- sets up default camera and lights
- set up webvr-polyfill, VREffect
- Add UI to Enter VR that calls WebVR API

Properties
- **behaviors** - Array fo components with tick methods that will be run on every frame
- **camera** - active Three.js camera
- **canvas** - reference to the canvas elem
- **isMoble** - in a mobile env or not
- **renderer** - active THREE.WebGLRenderer
- **renderStarted** - has it started rendering
- **effect** - Renderer for VR created by passing active renderer into THREE.VREffect
- **systems** - instantiated systems
- **time** - global uptime of the scene in seconds
- **loaded** - event fired when all nodes have loaded

## Animations
defined by attaching an `<a-animation>` element as a child of an entity to animate it, roughly based on the [web animations specs](https://www.w3.org/TR/web-animations/)

Properties
- **attribute** - the component to be animated, ie rotation, light.intensity
- **begin** - name of the event to wait on before beginning animation
- **delay** - delay or event name to wait on before starting the animation
- **direction** - Direction of the animation
- **dur** - duration of the animation
- **easing** - easing function for the animation
- **end** - event name to wait on before stopping animation
- **fill** - determines effect of animation when not actively in play
- **from** - starting value
- **repeat** - number of times to repeat
- **to** - end value

## General
* **registerShader** - register a custom shader
  - takes a schema property, that defines uniforms and attributes the shader will use
    - **color** - vec3 uniform type, automatically converts colors to vec3 format
    - **number** - maps to GLSL float
    - **time** - float uniform type, the material component will continuously update the shader with the global scene time
    - `vec2, vec3, vec4` - maps to GLSL equivalents
  - `this.materal` - provides access to the desired material
  - `vertexShader, fragmentShader` - properties to specify custom shader programs as a string
* 


## Tips
* Make use of the asset management system to benefit from browser caching and preloading. Trying to fetch assets while rendering is slower than fetching all assets before rendering.
* Use the stats component to keep an eye on various metrics (FPS, vertex and face count, geometry and material count, draw calls, number of entities. We want to maximize FPS and minimize everything else.)
* If using models, look to bake your lights into textures rather than relying on real-time lighting and shadows.
* Generally, the fewer number of entities and lights in the scene, the better.

## Links
* [aframe boilerplate](https://github.com/aframevr/aframe-boilerplate/)
