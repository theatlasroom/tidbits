# Elm
## Command line tools
* **elm-repl**: used to explore simple elm expressions
  - compiles elm code to javascript, so requires node.js
  - `:help` - help and more info
  - `:exit` - exit the repl
  - `\` - lets us split onto multiple lines
* **elm-reactor**: helps build elm projects
  - `--port` - specify the port you want to run the application at
  - `--address` - lets you replace localhost with some other address. For example, you may want to use elm-reactor --address=0.0.0.0 if you want to try out an Elm program on a mobile device through your local network.
  - **elm-make**: builds elm projects, it can compile to html or javascript
    - `--output` - specify the output file
  - **elm-package** - download and publish packages from the package catalog
    - dependencies are added to your elm-package.json file
    - `install` - install a dependency
    - `publish` - publish a library
    - `bump` - bump version numbers based on an api change
    - `diff` - get the difference between 2 apis

## Core langauge
**Values**
- elm uses the `++` operator to concat strings
- elm distinguishes between integers and floats
  * `/` - used for floating point division
  * `//` - used for integer division

**Functions**
- functions are defined in the form
`isNegative n = n < 0`
- arguments are separated with spaces
`isNegative 4`
`add 3 4`

**If expressions**
- used for conditional logic
- in the form `if <expr> then <expr> else <expr>`
- there is no notion of 'truthiness', so numbers, strings and lists cannot be used as boolean values

**Lists**
- lists are the most common data structure, they hold a sequence of related things
- all values must have the same type in a list
- `> numbers = [1,3,2,4]`
  `> List.sort numbers
     [1,2,3,4]`


- functions
  * `List.isEmpty <list>` - check if the list is empty
  * `List.length <list>` - return the length of the list
  * `List.sort <list>` - sort the list
  * `List.reverse <list>` - reverse the list
  * `List.map <function> <list>` - apply the function to each element in the list

**Tuples**
- can hold a fixed number of values and each value can have any type
- used to return more than one value from a function
 - this function gets a name and gives a message for the user
`import String
goodName name =
  if String.length name <= 20
  then (True, "name "accepted)
  else (False, "name is too long")

goodName "Tom"
`

**Records**
- a set of key-value pairs, similar to js / python objects
- `point = { x = 3, y = 4}
   point.x`
- we create records using curly braces and access fields using a dot
- records can be access by name ie get the record where the name is bill
  `> bill = { name="Gates", age=57 }
   > .name bill
      "Gates"
   > List.map .name [bill, bill]
      ["Gates", "Gates"]`
- you can use pattern matching to make functions with records
  - in this example the function could be used on any record that has an age field that holds a number
  `> under70 {age} = age < 70
   > under70 bill
      True
   > under70 { type="Trex", age=60 }
      False`
- we can use the pipe to update the value of a field
  `> { bill | name="Nye" }`
  this returns a new record, internally elm will share all the data that isnt changed

- Records in Elm are similar to objects in JavaScript, but there are some crucial differences. The major differences are that with records:
  * You cannot ask for a field that does not exist.
  * No field will ever be undefined or null.
  * You cannot create recursive records with a this or self keyword.
  * Elm encourages a strict separation of data and logic, and the ability to say this is primarily used to break this separation. This is a systemic problem in Object Oriented languages that Elm is purposely avoiding.
  * Records also support structural typing which means records in Elm can be used in any situation as long as the necessary fields exist. This gives us flexibility without compromising reliability.  

## Architecture
### Pattern
**Model** - the state of the application
**Update** - a way to update your state
**View** - a way to view your state as HTML

Skeleton
`import Html exposing (...)

-- MODEL

type alias Model = { ... }

-- UPDATE

type Msg = Reset | ...

update : Msg -> Model -> Model s
update msg model =
  case msg of
    Reset -> ...
    ...

-- VIEW

view : Model -> Html Msg
view model =
  ...
`

### User input

### Libraries
- `Html` - full access to HTML5 as elm functions
 * Html functions take 2 inputs, a list of attributes and a list of child nodes


## Useful links
* [Learn elm in y minutes](https://learnxinyminutes.com/docs/elm/)
* [elm + electron](https://medium.com/@ezekeal/building-an-electron-app-with-elm-part-1-boilerplate-3416a730731f#.jb717cy6q)
