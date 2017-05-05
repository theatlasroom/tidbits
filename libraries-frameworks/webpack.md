# Webpack
Module loader in the vein of require and browserify
* install via npm: npm install -g webpack
* create webpack.config.js file
* resolves the order of loading modules
* use module: [loaders:{}] to set babel transpiler config

## 2.0
### Caching
* webpack allows the use of output placeholders to substitute information generated during the build
  - `[name]`: file / asset name
  - `[hash]`: a unique hash generated for each webpack build
  - `[chunkhash]`: a hash generated for a single file, if the file has not changed, this hash will remain the same
* use `[chunkhash]` to enable long-term caching of static resources
  - a manifest json file is produced to map a resource to its cached output file
  - the manifest file can be inlined into the page

## Dev server

## Hot module replacement
HMR exchanges, adds or removes moduleits while an application is running without a page reload

## loaders
allow us to perform actions on our files
* **babel-loader** - transform es2015 and jsx
* preloaders are applied to the code before it gets transformed
* when you have an array of loaders configured for a matching test, the loaders are executed from last to first

## Plugins
* `DefinePlugin()` - implements a regex that searches our source and replaces variables defined in a key(name of variable)-value(name in the source code) object
  - by convention surround the replaced variables with 2 underscores either side ie NODE_ENV => __NODE_ENV__

## Angular
### 1.x
* need to make changes since webpack uses commonJS modules
* need to *require* angular first

## Notes
* [hjs-webpack](https://github.com/HenrikJoreteg/hjs-webpack) provides helpers and presets to set up your wepback config
* don't include minified file dependencies, this will cause the **--optimize-minimize** to take forever to complete building.
* [SurviveJS - webpack / react](http://survivejs.com/webpack/advanced-techniques/configuring-react/)
* [Webpack - the confusing parts](https://medium.com/@rajaraodv/webpack-the-confusing-parts-58712f8fcad9)
* [HMR](https://medium.com/@rajaraodv/webpacks-hmr-react-hot-loader-the-missing-manual-232336dc0d96)
