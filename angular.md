# Angular
## Unit Testing

## E2E Testing

## Directives
[Sweet explanation at Sitepoint](http://www.sitepoint.com/practical-guide-angularjs-directives-part-two/)

Directives are custom elements, or markers in the DOM that encapsulate and attach some custom behaviour. Directives allow to create new syntax in your markup.

Declare a directive on a module using the `module.directive('name', closure)` syntax, the name is always declared in camelcase but in your html it is called using snake-case

There are four types of closures possible
* E - Element `<custom-element></custom-element>`
* A - Attribute `<div custom-element></div>`
* C - Class `<div class="custom-element"></div>`
* M - Comment `<!--directive:custom-element-->`

By default a directive has access to its parent scope, the other options are:
* child scope: `scope: true` prototypically inherited from the parent
* isolated scope: `scope: {}` a new scope that exists on its own

You can access attributes in the parent scope by:
* one-way binding: `scope:{attr: @parentattr}`, this passes a string to the isolated scope, if both attrs have the same name you can just use `@` without a name
* scope model: `scope:{attr: '='}`, assigns a scope model to the attribute
* execute functions: `scope:{someFunction: '&amp;'}`

### Link function
The link function is used to access the scope of the directive. The function is used to bind to DOM elements in the directive, create watchers on properties and updating the DOM.
It takes 3 parameters
* scope: the scope passed to the directive
* elem: a jquery/jqlite wrapped element the scope is applied to
* attrs: a normalised list of any attributes declared for the directive

* The template needs to be compiled against a scope to do anything
* By default a directive doesnt get a new child scope, it inherits the parent scope, if you declare it in a controller, it will use that controllers scope

### Compile function
Used to apply an DOM transformation before the link function, the compile function has no access to the scope. The compile function can be used to gain a performance boost when using a cloned directive ie ng-repeat. The compile function will run just for template, but the link function executes for each instance of the clone

### Transclusion

### Controller

### Simple example
`app.directive('helloWorld', function() {
  return {
      restrict: 'AE',
      replace: 'true',
      template: '<h3>Hello World!!</h3>'
  };
});`
