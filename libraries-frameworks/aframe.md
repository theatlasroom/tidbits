# Aframe
[A-Frame](https://aframe.io)
- Open source frameowrk for 3d and VR content built on three.js
- Built by MozVR team for prototyping WebVR content
- Easily create multiplatform VR scenes for desktop, Oculus rift and mobile
- Based on the `entity-component-system pattern (ECS)`, focused on composability over inheritance
  * `entity`: a general purpose object that does and renders nothing
      - Represented via an HTML element ie `<a-entity>`
  * `component`: a resuable module that is plugged into entities to provide appearance, behaviour and/or functionality
      - represented via a html attribute
      - component properties are represented by values defined in a attribute
  * `system`: provides global scope, services and management for components
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
* `<a-animation>` - animates an entity
* `<a-assets>` -
  - useful for caching assets that are needed within the scene, ie images.
  - define the asset in the entity and give the asset an id, refer to the asset using the id selector `#asset`
* `<a-camera>` - used to explicitly define a camera, if it is not there then the default camera is used
* `<a-cursor>` - used to interact with entities
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

## Components
* `Stats` - displays a UI with performance related metrics, applies only to the `<a-scene>` element
  - `<a-scene stats></a-scene>`
  - `fps`
  - `raf latency` - requestAnimationFrame
  - `Textures` - threejs textures
  - `Programs` - number GLSL shaders in the scene
  - `Geometries`
  - `Vertices`
  - `Faces`
  - `Calls` - number of draw calls on each frame
  - `Load time` - how long it took for the scene to start rendering in ms
  - `Entities` - number of A-frame entities

## Tips
* Make use of the asset management system to benefit from browser caching and preloading. Trying to fetch assets while rendering is slower than fetching all assets before rendering.
* Use the stats component to keep an eye on various metrics (FPS, vertex and face count, geometry and material count, draw calls, number of entities. We want to maximize FPS and minimize everything else.)
* If using models, look to bake your lights into textures rather than relying on real-time lighting and shadows.
* Generally, the fewer number of entities and lights in the scene, the better.

## Links
* [aframe boilerplate](https://github.com/aframevr/aframe-boilerplate/)
