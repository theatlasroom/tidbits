# Javascript

## General
* Cross platform OO scripting language that executes within a host environment
* The core provides a standard library fo objects such as Array, Date, Math and a set of operators, control structures and statements
* The core can be extended for different purposes
  - Client side JS: adds objects to control a browser and its DOM, such as responding to user events, page navigation or adding elements to the DOM
  - Server side JS: provides objects for allowing JS to communicate with a DB, perform file maniupulations etc
* Dynamic, loosely typed
* Uses a prototype-based model to provide dynamic inheritance.
* Properties and methods can be added to any object dynamically
* JS is standardized by ECMA international,  TC39 committee. ECMAScript behaves the same way in all applications that support the standard
  - ECMA provides standards for, language syntax, error handling mechanisms, Types, the global object, a prototype inheritance mechanism, built in objects and functions (JSON, Math, Array...), strict mode
  - the DOM is standardized by W3C not ecma
  - Other apis include: XMLHttpRequest, CSS object model, WebWorkers, WebSockets, Canvas 2D

## Scopes, chains, closures
* lexical scoping - this is the scope that is created within a function
    - **var** is used to define a variable lexically scoped
* block scoping - the scope created within curly braced blocks
    - **let** and **const** are used to define block scope variables
* JS also has scopes global, with, catch and eval scopes
* Scopes can be nested, both lexical and block scopes can contain a nested scope
    - ie if nested in a function, function nested ina function etc
* Each nested scope has access to the outer scopes variables, but not vice versa
    - sibling nested scopes cannot access each others variables
* **Scope chain** is a tree that maps the nesting of scopes within a function
   ` (global)
        ↑
        |
       foo()
      var bar
        ↑
        |
       zip()
     var quux`
* All JS runtimes must have a global scope object
    - **window** for the browser
    - **global** for node
* When assigning a variable without using var, let or const, the variable is assumed to exist in an outer scope
    - the runtime will search upwards through the scope tree to try and find the variable, if it can't then it will create it on the global scope object
* **Shadowing** - redefining a variable in a inner scope, the inner scope can only access its own version of the variable
* **closures** - an inner function accessing a variable in its outer scope is said to **close over** the variable
* Most JS runtimes use the **mark and sweep** algorithim for garbage collection
    - references to memory (variables, functions etc) are marked if they are still reachable from active code
    - any unmarked reference is swept into the garbage and the memory is released
    - in the memory timeline of chrome dev tools, GC appears as a sudden drop
    - GC events block the main thread

### Syntax
#### Grammar and types
* case sensitive and uses the unicode character set
* instructions are called *statements* and are seperated by a semicolon(;)
* Spaces tabs and newline characters are all whitespace
* Scripts are scanned from left to right and converted into a sequence of input elements which are tokens, control characters, line terminators, comments or whitespace
* var, let and const are used to declare variables
  - let declares a block scope variable
  - const declares a read-only named constant
  - variables declared by var or let that have no initial value are set to *undefined*
  - undefined value behaves as false in a boolean context and NaN in a numeric context
  - null behaves as 0 in a numeric context and false in boolean

#### Control flow and error handling
* Just about any object be thrown in JS, its best to throw one of the specifically created types for this
  - ECMAScript exceptions
  - DOMException and DOMError
* You can specify an object when you throw an exception
`// Create an object type UserException
function UserException(message) {
  this.message = message;
  this.name = "UserException";
}

// Make the exception convert to a pretty string when used as a string
// (e.g. by the error console)
UserException.prototype.toString = function() {
  return this.name + ': "' + this.message + '"';
}

// Create an instance of the object type and throw it
throw new UserException("Value too high");`
* Use the try / catch statement to execute a block and catch exceptions
  - the finally block can be used to execute code that runs regardless of an exception being caught or not
  - ErrorType(message) object can be used to throw an error and supply a message to be displayed

#### Data types
* there 7 data types defined in ECMAScript
* the 6 primitive data types are
  - Boolean: true|false
  - null: a keyword to denote a null value. since JS is case-sensitive Null and NULL etc are not the same
  - undefined
  - Number: 42|3.14159
  - Stirng: "Hello world"
  - Symbol: provides unique and immutable instances
* the 7th data type is Object
* Expressions containing the *+* operator with numeric and string value automatically convert the numerics to strings
* literals are used to represent values, they are fixed values you provide in your script
  - Array Literal: a list of 0 or more expressions which represent an element in the array enclosed by []. An arary literal used in a function is created each time the function is called
  - Boolean Literal: true/false
  - Floating point Literal: decimal integer that can be signed, fraction or an exponent (.1e-23)
  - Integers: number expressed in decimal, hex(ox), octal(0o) or binary (0b)
  - Object Literal: list of 0 or more pairs of key/values enclosed in {}. Property names can be any string including the empty string
  - RegExp Literal
  - String Literal
* `String.charCodeAt(index)` - returns the utf16 representation of the character at the index selected

#### [Typed arrays](http://developer.mozilla.org/en-US/docs/Web/Javascript/Typed_arrays)
Provide access to binary data, have been standardized across most browsers.
There are various types such as **Uint8Array** (similar to nodejs buffers) and Int8Array (can store +ve and -ve integers)

Typed arrays use [**ArrayBuffers**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer) underneath to the raw bytes.
To access their data, you need to create a typed array (a view) thorugh which to access the data.
- the `.buffer` property returns the underlying arraybuffer used for the view

#### Notes
* *debugger* can be used to invoke any available debugger if one exists ie like setting a breakpoint
* Octal numbers use a leading 0 followed by a lower/uppercase "O" ie 0o644 => 420
* Hexadecimal numbers use a leading 0 followed by a lower/upper case "X" 0xA => 10
* Hexadecimal escape sequences '\xA9' => "©"
* Unicode escape sequences '\u00A9' => "©"
* Regex literals /ab+c/g


## ES6

### Promises
* use the .then().catch() form to catch any errors within promise chains
* use Promise.all(promise1, promise2).then() - this will pass the results of both promises as an array to the then block
* if you have promises dependent on previous results, nest with Promise.all
`firstThingAsync()  
  .then(function(result1) {
    return Promise.all([result1, secondThingAsync(result1)]);
  })
  .then(function(results) {
    // do something with results array: results[0], results[1]
  })
  .catch(function(err){ /* ... */ });
`

## Links
* [Anti Patterns](http://www.datchley.name/promise-patterns-anti-patterns/)
* [More antipatterns](http://taoofcode.net/promise-anti-patterns/)

## Testing - Jasmine
Keep your modules small
Always throw / return errors when you need to and check for them in your tests
- success, error, expected and unexpected data
Describe block - module
it block - function
  - passing the done param forces jasmine to assume it is an async function

mocks
- sinon, rewire, node-tap, require-inject
- should only be used when the final result is to call an external service ie db / external api
- used to verify a call against an external service

spies

doubles

Code coverage
- istanbul
