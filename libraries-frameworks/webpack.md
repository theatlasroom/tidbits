# Webpack
Module loader in the vein of require and browserify
* install via npm: npm install -g webpack
* create webpack.config.js file
* resolves the order of loading modules
* use module: [loaders:{}] to set babel transpiler config

## Dev server

## Hot module replacement
HMR exchanges, adds or removes moduleits while an application is running without a page reload

## loaders
allow us to perform actions on our files
* `babel-loader` - transform es2015 and jsx
* preloaders are applied to the code before it gets transformed
* when you have an array of loaders configured for a matching test, the loaders are executed from last to first

## Angular
### 1.x
* need to make changes since webpack uses commonJS modules
* need to *require* angular first

## Notes
* [hjs-webpack](https://github.com/HenrikJoreteg/hjs-webpack) provides helpers and presets to set up your wepback config
* don't include minified file dependencies, this will cause the `--optimize-minimize` to take forever to complete building.
* [SurviveJS - webpack / react](http://survivejs.com/webpack/advanced-techniques/configuring-react/)
