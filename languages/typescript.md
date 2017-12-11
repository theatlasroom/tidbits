# Typescript
* Superset of JS that can be compiled using the typescript compiler
* annotations are lightweight ways to record intended contract of a function or variable
  - passing the wrong type of variable throws a type error
* Interfaces describe the structure of a type
  - 2 types are compatible if their internal structure is compatible
* Classes are supported and can be used to implement an interface
  - adding `public` to an argument allows us to automatically create properties with that name

## Types
* Supports javascript data types `boolean`, `number`, `string`
  - `let <variable>: <type> = <value>;`
* Arrays can be typed or generic
  - ReadonlyArrays are identical, but with all *mutating* methods removed
  - readonly arrays can be overridden with a type assertion
```
// typed array
let list: number[] = [1,2,3]

// generic array type
let list: Array<number> = [1,2,3]

// Readonly
let a: number[] = [1, 2, 3]
let ro: ReadonlyArray<number> = a;
```

* Tuples define an array where a fixed number of elements is known but dont have to be the same
```
// declare a tuple type
let x: [string, number]
// initialize
x = ["hello", 10]
```
  - retrieving a tuple element by index returns a the correct type
* Enums can be used to give nicer names to numeric values
  - enum begin counting at 0
```
enum Color {Red, Green, Blue}
let c: Color = Color.Green
```
  - setting a single member of the enum will start the count from that value
* type `any` opts out of compile time checks
* `void` can be set as the return type of a function
* type `never` is used for types that are never reached such as functions that always throw or are infinite loops

## Interfaces
* Typescript uses duck typing, interfaces define the shape of types
* optional properties can be specified with a `?`
```
interface SquareConfig {
  color?: string;
  width?: string;
}
```
* Read only properties can be specified with `readonly`
  - readonly properties can be assigned via the constructor by assigning an object literal, but cannot be changed afterwards
```
interface Point {
  readonly x: number;
  readonly y: number;
}
```
* interfaces can describe function types
  - parameters are checked one at a time and so their names do not need to match, just their position and type
```
interface SearchFunc {
  (source: string, subString: string): boolean;
}

let mySearch: SearchFunc;
mySearch = function(source: string, subString: string){
  ...
}
```
* interfaces can be implemented by class types
```
interface ClockInterface {
  currentTime: Date;
  setTime(d: Date);  
}

class Clock implements ClockInterface {
  ...
}
```
* interfaces can extend multiple interfaces, combining all the properties
