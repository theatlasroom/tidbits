# Webpack
Module loader in the vein of require and browserify
* install via npm: npm install -g webpack
* create webpack.config.js file
* resolves the order of loading modules
* use module: [loaders:{}] to set babel transpiler config

## Dev server

## loaders
allow us to perform actions on our files
* `babel-loader` - transform es2015 and jsx

## Angular
### 1.x
* need to make changes since webpack uses commonJS modules
* need to *require* angular first

## Notes
* [hjs-webpack](https://github.com/HenrikJoreteg/hjs-webpack) provides helpers and presets to set up your wepback config
* don't include minified file dependencies, this will cause the `--optimize-minimize` to take forever to complete building.
