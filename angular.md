# Angular
## Overview
### Scope and binding
When you create a data binding in your view to a variable that is available on $scope, angular will create an internal 'watch'. Angular will watch the changes in the variable. Angular will compare the current value of with the last value returned from the watch to determine if it has been changed.

* `$watch()`: creates a watch on a variable, takes:
  - a value function (returns the value to be watched)
  - a listener
* `$digest()`: iterates through all watches in the scope object and its child scope objects and checks if any of the watched variables have changed. If a variable has changed, the relevant listener function is executed
* `$apply()`: used to execute some code and then call $scope.$digest() after which updates all watches.

## Unit Testing

## E2E Testing

## Directives

### Built in
* ng-class: dynamically set css classes
`<elem ng-class="class: condition" />`
`<elem class="ng-class: expression" />`

### Custom
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

## Packages
### Formly
* Adding attrs to a form field:

### UI Router
[Stateful modals](http://www.sitepoint.com/creating-stateful-modals-angularjs-angular-ui-router/)

Example opening a modal on state change using angular-strap
Use this in the state config
`onEnter: function($stateParams, $state, $modal) {
    $log.log("onEnter");
    $modal({
        templateUrl: "js/partials/some-template.html",
        resolve: {
          // resolve deps needed in the controller
        },
        controller: function($scope) {
          $scope.dismiss = function() { $scope.$dismiss(); };
          $scope.save = function() { };
          $state.go('home');                
        }
    });
}`


* To load a state within another view, make sure to specify the view `<div ui-view="modal" autoscroll="false"></div>`
* When a state is activated, its templates are automatically inserted into the `ui-view` of its parent state's template. If it's a top-level state—which 'contacts' is because it has no parent state–then its parent template is index.html.
