# ReasonML
## General
- [OCaml](http://ocaml.org/) syntax that compiles to JS, and integrates into the npm ecosystem
- Compiles to JS using [BuckleScript](https://bucklescript.github.io/)
- Static typed, opt-in side effects and mutation
- accepts raw JS
- Open source project from Facebook

## Syntax
### Basics
* Mostly the same as JS with a few exceptions
* Integers: 32 bit, will be truncated
  - convert JS numbers to float to avoid truncation
* Strings
  - use `"`
  - concatenation: `++`, `"Hello" ** "World"`
  - special characters need to be escaped
  - quoted strings `let greeting = {|Hello World|}`
    * can span multiple lines
    * do not require escaping
    * provide hooks for pre-processors
  - operations can be mixed and matched with `Js.String`
* Characters, use
  - do not support unicode or UTF-8
  - string to char: `"a".[0]`
  - char to string: `String.make(1, 'a')`
* Floats
  - addition: use the `+.` operator: `23.0 +. 1.0`
  - division: use `/.`
  - multiplication: use `*.`
  - exponentiation: `**`
* Immutable lists
   - `[1, 2, 3]`
   - prepend: `[item1, item2, ...theRest]`
* Arrays: `[|1, 2, 3|]`
* Records: `type player = {score: int}; {score: 100}`
* Comments only use `/* */`
### Binding
* Ability to assign a name to a value, uses the `let` keyword
```
let greeting = "Hello!"
let score = 10;
let newScore = 10 + score;
```
* Bindings can be scoped with braces `{ }`
```
if (displayGreeting){
  /* message is only accessible within this block */
  let message = "Enjoying the docs?";
  print_endline(message)
};
```
  - bindings are *immutable*
  - bindings can be *shadowed*, assigning a new binding to a name that already exists
  - anonymous scopes can be created for bindings
```
let message = {
  let start = "start of message";
  let end = "end of message";
  start ++ " " ++ end
}
```
### Types
* all reason code is typed
* types can be inferred, but can also be explicit
```
let score = 10; // inferred int type
let score: int = 10; // explicit int
```
* any expression can be wrapped in parentheses and annotated with types
```
let myInt = (5: int) + (4: int);
let add = (x: int, y: int) : int => x + y;
```
* types can be aliased
```
type scoreType = int;
let x: scoreType = 10;
```
* *bool* can be `true` or `false`
  - structural equality `==` compares data structures deeply
  - referential equality `===` compares shallowly, favour this over structural checks
  - JS true/false is not the same as reason true/false
    * convert before trying to use them
    * `Js.true_` and `Js.false_` correctly compile
    * `Js.Boolean` exposes the js boolean type
    * reason bool to js Boolean:`Js.Boolean.to_js_boolean`
    * JS boolean to reason bool:`Js.to_bool`
  - compiles to `1` or `0`
* *Tuples*, immutable ordered fix sized, used for passing around multiple values
```
let coords = (0, 1, 0);
let typedCoords: (int, int, int) = (0, 1, 0);
type coords4d = (float, float, float, float);
let c: coords4d = (1.0, 2.0, 3.0, 0.0);
let (_, y, _) = c; // destructure y
```
  - should not be mutated
  - should be used for local, short lived values. prefer records for long lived data structures
* *Records* similar to js objets, but immutable by default, fixed field names and types
```
type person = {
  age: int,
  name: string,
}

 /* Person type inferred */
let me = {
  age: 5,
  name: "Big reason"
};
```
  - access fields using dot notation
  - require an explicit declaration for the type
  - definitions can be in separate files from usage
```
/* School.re */

type person = {age: int, name: string};

/* example.re */
let me: School.person = { age: 20, name: "Big Reason"};
```
  - the spread operator can be used to create new records, but can not add new fields
  - fields can be specified as mutable where needed
```
type mutablePerson = {
  name: string,
  mutable age: int
};

type immutablePerson = {
  name: string,
  age: int
};

let baby: mutablePerson = { name: "Lol", age: 5 };
baby.age = baby.age + 1;

let adult: immutablePerson = { name: "YEAH", age: 18 };
```
* *Variant* expresses variations
```
type myVariant =
  | Yes
  | No
  | PrettyMuch;

let areYouCrushingIt = Yes;

let message =
  switch (areYouCrushingIt) {
  | No => "No worries. Keep going!"
  | Yes => "Great!"
  | PrettyMuch => "Nice!"
  };

/* Yes, No, PrettyMuch are `constructors` */
```
  - constructors of a variant need to be capitalized
    * they can hold extra data `... | Instagram(string | Facebook(string, int);`
  - switch expressions can be used to enumerate each possible case of a variant
  - like records, they require an explicit definition
  - ``option(`a)`` comes from the standard library and returns ``None | Some(`a)``
* *List* homogenous, immutable singly linked list
```
let myList: list(int) = [1,2,3];
let newList = [0, ...myList];
```
  - use the `...` spread operator to prepend lists
  - use *List.concat* to combine multiple lists
  - use *List.nth* to access arbitrary items
* *Array* similar to lists, but mutable, arrays map to `Js.Array`
```
let myArr: array(string) = [|"One", "Two", "Three"|]
```
* types can be parametized, similar to how *generics* are used
```
type someFunc('a) = ('a,'a,'a);
```
* types can be mutually recursive
```
type student = {taughtBy: teacher}
and teacher = {students: list(student)};
```

### Functions
* declared with a parenthesised arrow and return expression `() =>`
* functions can automatically be curried
```
let add = (x, y, z) => x + y + z;
add(1,2,3); /* returns 6 */
 ```
* every function takes an argument, the unit argument `()` is used when we have nothing to pass into the function
* labels can be used to specify which arguments you are passing to a function
  - labelled arguments can be passed in any order
  - optional arguments automatically get wrapped in an *option* type, ensuring they can return None or Some(type)
    * a trailing unit parameter `()` is required
  - optional arguments can be forwarded to another function without checking if it is None or Some
  - optional arguments can have a default value `...~color="red",`
```
let add = (~x, ~y) => { ... } /* labelled arguments */
add(~x=5, ~y=10);

/* aliased, labelled arguments */
let sub = (~xCoord as x, ~yCoord as y ) => x - y
sub(~xCoord=10, ~yCoord=5);

/* optional labelled arguments */
let div = (~x, ~y=?, ()) => {
  switch (y){
    | None => x / 1
    | Some(divisor) => x / divisor
  }
};
div(~x=10);
div(~x=10,~y=2);

/* forward the optional radius argument without checking if it is there */
let result = drawCircle(~color, ~radius=?payloadRadius, ());
 ```
* the `rec` keyword is used to specify a recursive function
  - mutually recursive functions are joined with the `and` keyword
```
/* single recursive function */
let rec neverEndingStory = () => neverEndingStory();

/* mutually recursive functions */
let rec callSecond = () => callFirst()
and callFirst = () => callSecond();
```
### Control structures
* `if / else` are expressions, they evaluate to the body of the match
  - ternary's can also be used in place
* omitting the final `else` implicitly adds a unit expression `else { () };`

```
let res = if (something) { returnSomething() } else { returnSomethingElse() }

if (something) {
  doSomething
}; /* implicit else { () }; */

```

### Modules
Modules can be passed to functions (not all functions), they can only be passed to _functors_

Functors:
* Functors use the *module* keyword instead of *let*
* Take a module as an argument and return another module
* map from one module to another
* require annotating arguments
* their name must start with a capital


* Helpful - [reasonml-functors](http://2ality.com/2018/01/functors-reasonml.html)

## Interop
* Bucklescript interoperation with JS, useful for binding JS libraries into the reasonml / ocaml world.
* Gives the ability to declare a FFI from reasonml to JS
* Uses the same syntax that OCaml uses for C bindings

### Operators
General operators
```
[@bs.new] /* create a new instance of an object */
[@bs.val] /* define a variable or function */
[@bs.send] /* call a method on an object */
[@bs.send.pipe] /* place the main argument a the end of the function call, allowing the use of |> */
[@bs.obj] /* Create a JS object from labelled args */
[@bs.splice] /* call a function with a variable number of the same type of argument */
```

Raw javascript dumped straight into reason
```
[%%raw "var a = 5"]
```
Saving a raw js expression into a reason variable (generally not type safe)
```
let add = [%raw {|
 function(b){ ... }
|}];
```
Annotated raw expression, better for type safety
```
let add: ((int, int) => int) = [%raw {| function(a,b){ ... } |}];
```
Mapping a value
```
[@bs.val] external sqrt : float => float = "Math.sqrt";

/* using the function */
let four = sqrt(2.0);
```

## ReasonReact
react bindings for reasonml

### General
* Doesnt require classes, records are used to create components with the `make` function, field such as `render`, `initialState` and `didMount` can be overidden for the component
  - `ReasonReact.statelessComponent`
  - `ReasonReact.reducerComponent` (stateful)
  - `ReasonReact.null` returns a null value
  - `ReasonReact.string` converts a string to a `reactElement`
  - `ReasonReact.array` converts an array to a reactElement
  - `render` - returns a `ReasonReact.reactElement`, `<div />`, `<Component />` etc
```
let component = ReasonReact.statelessComponent('Test')
...
let make = (~name, _children) => {
  ...component, /* spread defaults into the function */
  render: _self => <div> {ReasonReact.string(name)}</div>
}
```
* Rendering / calling a component without JSX
```
ReasonReact.element(Test.make(~name="Some name", [||]))
```
* Props are just labelled arguments to make, they follow normal rules of reason arguments, except the last prop must be `children`
  - optional props can be set using `=?` ie `<Foo name="Reason" age=?ageFromProps />`
* `self`
   - equivalent to JS `this`
   - a record that contains `state`, `handle` and `send` and is passed to lifecycle events and render
* `ReactDOMRe.createElement` compiles to `React.createElement`
  - use `ReasonReact.createDomElement` if you need an escape hatch

### Events
* `self.send` - update state in a callback
* Callback without state update
```
/* call the function pass in via props */

let component = ...
let make = (~name, ~onClick, _children) => {
  ...component,
  render: (self) => <button onClick=onClick />
}

/* intercept value before calling callback */

let component = ...
let make = (~name, ~onClick, _children) => {
  let click = (event) => onClick(name);
  {    
    ...component,
    render: (self) => <button onClick=onClick />
  }
}
```
* Callback with state
  - wrap the callback with `self.handle`
  - pass the whole `self` record if you are forwarding to a handler
```
let component = ...
let make = (~name, ~onClick, _children) => {
  let click = (event, self) => {
    onClick(event);
    Js.log(self.state);
  };
  {
    ...component,
    initialState: ...
    render: (self) => <button onClick={self.handle(click)}
  }
}
```
* Callback with state with multiple arguments
```
/* handle expects to wrap a function that only takes 1 argument */

let handleSubmitEscapeHatch = (username, password, event) =>
  self.handle(
    (tupleOfThreeItems, self) => doSomething(tupleOfThreeItems, self),
    (username, password, event),
  );
```

## Libraries
* [Arg](https://reasonml.github.io/api/Arg.html) - CLI command parsing

## Links
* [Playground](https://reasonml.github.io/try.html)
* [Cheatsheet](https://reasonml.github.io/docs/en/syntax-cheatsheet.html)
* [ReasonML: functions](http://2ality.com/2017/12/functions-reasonml.html) - deep look at ReasonML functions
* [ReasonML documentation](https://reasonml.github.io)
* [Redex - package index](https://redex.github.io)
* [React + reason](https://itnext.io/a-journey-to-reason-c408a87a54de)
* [ReasonReact](https://reasonml.github.io/reason-react)
* [Component styling api](https://medium.com/@tahini/building-a-reasonml-component-styling-api-part-1-837177655a5c)
* [David Gomes - expoloring interop](https://www.youtube.com/watch?v=-C-mv_Mc1mQ)
* [Reasonconf videos](https://www.youtube.com/channel/UCtFP_Hn5nIbZY4Xi47qfHhw/playlists)
