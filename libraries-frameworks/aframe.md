# Aframe
## General
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
  * `system`: provides global scope, services and management fo components
  * Lets us build complex entities with rich behaviour by plugging different reusable components into the sockets on the entity

 
## Entities
* 

## Components
* `Stats` - displays a UI with performance related metrics, applies only to the `<a-scene>` element
  ** `<a-scene stats></a-scene>`
  ** `fps`
  ** `raf latency` - requestAnimationFrame
  ** `Textures` - threejs textures
  ** `Programs` - number GLSL shaders in the scene
  ** `Geometries`
  ** `Vertices`
  ** `Faces`
  ** `Calls` - number of draw calls on each frame
  ** `Load time` - how long it took for the scene to start rendering in ms
  ** `Entities` - number of A-frame entities

## Tips
* Make use of the asset management system to benefit from browser caching and preloading. Trying to fetch assets while rendering is slower than fetching all assets before rendering.
* Use the stats component to keep an eye on various metrics (FPS, vertex and face count, geometry and material count, draw calls, number of entities. We want to maximize FPS and minimize everything else.)
* If using models, look to bake your lights into textures rather than relying on real-time lighting and shadows.
* Generally, the fewer number of entities and lights in the scene, the better.

## Links
* [aframe boilerplate](https://github.com/aframevr/aframe-boilerplate/)
