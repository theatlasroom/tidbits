# GO
* [Go spec](https://golang.org/ref/spec)

## General
* Go code is all kept in a workspace
  - A workspace contains repos
  - Each repo contains one or more packages
  - Each package contains one or more .go files
  - At its root, a workspace contains 3 folders
    - `src`: go source files
    - `pkg`: package objects
    - `bin`: executable commands
* `go env GOPATH` outputs the current go path
* Every go program is made up of packages
  - By convention, the package name is the same as the last element of the import path -> math/rand files that being with package rand
  - when importing a package you can only refer to its exported names. Unexported names are private
* Programs start running in package `main`
* everything is pass by value (by default)
* must explicitly pass by reference ("&")
* public / private variables are declared by uppercase(first) / lowercase
  - a name that starts with an uppercase will be exported
* go routines - threads
* channels - communication and synchronisation between threads
* High level memory safe, garbage collected statically typed
* no classes or type inheritance
  - ad hoc type relationships via interfaces
  - any type that implements all the methods of an interface, automatically implements the interface

## Tools
* `go build` - build an executable
* `go test` - run tests for a package
* `go run` - run a go program
* `go get` - locate and install a
* `go tool fix` - updates programs that use old apis and rewrites them to use newer ones
* `go fmt` - automatic formatting of your code

## Syntax
### General
* the var statement declares a list of variables, the type comes last
  - `var <variable> <type>`
  - initialisation can be used to infer a type, ie
```
var foo = "hello" <T = string>
var c, python, java bool
```
  * it can include initializers, if so the type can be omitted
```
var i, j int = 1, 2
var c, python, java = true, false, "no!"
```
* Within a func, `:=` can be used as a shorthand to declare a variable
  - `x := 3`
  - in this style we can omit the type and var
  - a variable can only be declared once in a scope
* Types
  - bool
  - int in8 int16 int32 int64
  - uint uint8 uint16 uint32 uint64 uintptr
  - byte // alias for unit8
  - rune // alias for unit32 -> unicode code point
  - float32 float64
  - complex64 complex128 (made up of 2 floating point numbers, 2x float32 or 2x float64)
  - conversion is done with the expression `T(v)` - where T is any valid type
  - inference is done based on the value in the right hand side of the expression (even a function return)
* zero values:
  - 0 for numeric types
  - false for boolean
  - "" for strings
* Constants are declared using the `const` keyword
  - untyped constants are high precision
  - untyped constant will take the type needed by its context
* all integer types will over/underflow if you exceed their bounds
```
var x unit8 = 255 // range 0 - 255
x = x + 1 // result overflows and wraps around to 0

x = 4
x = x - 10 // result underflows and wraps around to 250
```
* floating point operations return `+Infinity or -Infinity`

### Functions
* a function can take 0+ arguments
```
func foo(x string, y bool) int {
  return 3;
}

foo(3, true)
```
* the type is declared after the variable name
* when 2 or more consecutive parameters share a type, you can omit all but the last type
  ` x int, y int, z int = x, y, z int`
* a function can return any number of results
```
func test....return y, x
a, b := test(param, param)`
_, b := foo() // discard variable a and extract b
```
* return values may be named
* a return statement without any values automatically returns the named return values in the function signature
  - only do this on short functions
* functions can be passed around like other values
  - they can be used as function arguments and return values
* functions can be closures, allowing the function to reference values outside its body

### Flow control
* go only has one looping construct - for statement
* flow control blocks have their own scope, they do not share variables in the outer scope they are defined in
* `for <init>;<condition>;<post>`
  - no braces around the statements
  - stops once the condition returns false
  - brackets are required
  - init, post are optional - `for sum < 1000 {}`
  - if you leave out the condition, you will have an infinite loop
  - `range` iterates over a slice or map
  ```
  pow := []int {1, 2, 4, 8, 16, 32, 64, 128}
  for i, v := range pow {
    fmt.Printf("2**%d = %d\n")
  }
  ```

    * the index or value can be skipped by using an underscore in its place, `_, value := range ....`
* if statement - () are optional, {} are needed
  - you can use shorthand statements in the condition `if v := math.Pow(x, n); v < lim {}`
  - variables declared in the statement, are available within the if and the else blocks
* Switch statement:
  - case body's break automatically unless they end with a `fallthrough` statement
  - default handles the default case
  - Switch can be used without a condition, this defaults to true, this can be useful for long if/then/else chains
```
t := time.Now()

switch {
case t.Hour() < 12:
  ...
case t.Hour() < 17:
  ...
default:
  ...
}
```

* Defer - defers the execution of a function until the surrounding function returns
  - useful for functions that perform cleanup
  - pushed onto a LIFO stack
  - [defer](https://blog.golang.org/defer-panic-and-recover)
  - there are 3 rules that determine the behaviour of a defer
    * **A deferred function's arguments are evaluated when the defer statement is evaluated**
    * **Deferred function calls are a executed in LIFO after the surrounding function returns**
    * **Deferred functions may read and assign to the returning functions named return values**
      - this can be useful for modifying the error return value of a function
  - `recover` is used within deferred functions to "catch" errors

### Pointers
* Pointers hold the memory address of a value
* `var p *int` - p is a pointer to a int value, its zero value is `nil`
  * `*p` provides access to the pointer for read / write
* `&` generates a pointer to a variable, `p = &i`
* functions with a pointer argument must take a pointer
* methods with pointer receivers can take either a value or a pointer
  - go will automatically infer (&v) when you invoke a method that requires a pointer receiver

### Structs
* a collection of fields
```
type Vertex struct {
  X int
  Y int
}
```
* struct fields are accessed via the `.` operator
* a struct literal lets createa struct by listing the values of the fields
  - `v = Vertex{X: 1} // Y defaults to Y:0`
  - not all fields are required and order does not matter

### Arrays
* `var a [10]int` - a is an array of 10 integers
* arrays length are part of their type, so arrays can not be resized
* a `slice` is a dynamically sized, flexible view into the elements of an array
  - `[m:n]` extracts a slice from m until n, both are optional, m defaults to 0, n defaults to the length of the slice
  - slices are references to an array
  - slices dont store any data, they just describe a section of an underlying array
  - slice literals can be used to build an array create a slice to it
    * slice literals have no length
    * `[]bool{true, true, false}`
  - `len(slice)` length is the number of elements in the slice
  - `cap(slice)` capacity is the number of elements in the underlying array, counting from the first element in the slice
  - the zero value of a slice is `nil`, len and cap are 0 in that case
  - slices can contains other slices
  - `make(type, length, capacity)` allocates a zeroed array and returns a slice that refers to the array
```
length := 10
a := make([]int, length)
```
    * useful for dynamically sized arrays
  - `.append(slice, values .... )` appends the values onto the slice provided and returns a new slice (with the appended values)

### Maps
* maps keys to values
* the zero value is nil
* the make function is used to create map of a given type
```
type Vertex struct {
  ...
}
m = make(map[string]Vertex) // create a map of Vertex structs, with a string key
m["Bell Labs"] = Vertex { ... }
```
* map literals require the keys
```
var m = map[string]Vertex{
	"Bell Labs": Vertex{
		...
	},
	"Google": Vertex{
		...
	},
}
```
* `delete(m, key)` - deletes the element at key `key` from map `m`
* `elem, ok = m[key]` - check if a key exists

### Methods
* a function defined on a type T, with a **receiver argument**
  - the receiver denotes the type the method applies to
  - the receiver appears between the func keyword and the method name
  - `func (v Vertex) Abs() float64 { ... }` - Abs method for type Vertex, return a float64
  - methods are functions
* methods can be defined on non-struct types
```
type MyFloat float64
func (f MyFloat) Abs(float64) { ... }
```
  - you can only declare a method with a receiver whose type is defined in the same package as the method
  - you can not declare a method with a receiver whose type is defined in another package including built ins like int
* you can declare a method with a **pointer receiver**
  - pointer receivers can modify the value the receiver points to
  - **value receivers** (non-pointer) receive a copy of the value
* for large structs methods avoid having to copy the struct multiple times, method also allow modification the receiver points to

## Packages
### fmt
Format output

### testing
Test framework

### Images
* [docs](chrome-extension://klbibkeccnjlkjkiokjodocebajanakg/suspended.html#ttl=The%20Go%20image%20package%20-%20The%20Go%20Blog&uri=https://blog.golang.org/go-image-package)

### time
time related functions

* Now() - UTC time

### math
Math libray

* rand
  * Intn - return a number
  * Seed - seed the number generator

* cmplx: complex numbers


## Glossary
* import - import go packages. By convention use the factored style `import ("fmt" "math" ...)`


### Useful links
* [Effective Go](https://golang.org/doc/effective_go.html)
* https://golang.org/doc/effective_go.html
* http://blog.golang.org/defer-panic-and-recover
* https://golang.org/src/encoding/json/example_test.go
* https://golang.org/pkg/fmt/
* https://golang.org/doc/articles/wiki/
* [Gobs of data](https://blog.golang.org/gobs-of-data)
* [Go web api example](https://github.com/caarlos0/go-web-api-example)
* [Go tooling workshop](https://github.com/campoy/go-tooling-workshop)
