# GO

- [Go spec](https://golang.org/ref/spec)
- [play-with-go.dev](https://play-with-go.dev/)
- [yourbasic/golang](https://yourbasic.org/golang/)
- [Writing an interpreter in GO](https://interpreterbook.com/)
- [Gitlab go style guide](https://docs.gitlab.com/ee/development/go_guide/index.html)

## General

- Go code is all kept in a workspace
  - A workspace contains repos
  - Each repo contains one or more packages
  - Each package contains one or more .go files
  - At its root, a workspace contains 3 folders
    - `src`: go source files
    - `pkg`: package objects
    - `bin`: executable commands
- `go env GOPATH` outputs the current go path
- Every go program is made up of packages
  - By convention, the package name is the same as the last element of the import path -> math/rand files that being with package rand
  - when importing a package you can only refer to its exported names. Unexported names are private
- Programs start running in package `main`
- everything is pass by value (by default)
- must explicitly pass by reference ("&")
- public / private variables are declared by uppercase(first) / lowercase
  - a name that starts with an uppercase will be exported
- go routines - threads
- channels - communication and synchronisation between threads
- High level memory safe, garbage collected statically typed
- no classes or type inheritance
  - ad hoc type relationships via interfaces
  - any type that implements all the methods of an interface, automatically implements the interface

## Tools

- `go build` - build an executable
- `go test` - run tests for a package
- `go run` - run a go program
- `go get` - locate and install a package
- `go tool fix` - updates programs that use old apis and rewrites them to use newer ones
- `go fmt` - automatic formatting of your code

## Syntax

### General

- the var statement declares a list of variables, the type comes last
  - `var <variable> <type>`
  - initialisation can be used to infer a type, ie

```
var foo = "hello" <T = string>
var c, python, java bool
```

- it can include initializers, if so the type can be omitted

```
var i, j int = 1, 2
var c, python, java = true, false, "no!"
```

- Within a func, `:=` can be used as a shorthand to declare a variable
  - `x := 3`
  - in this style we can omit the type and var
  - a variable can only be declared once in a scope
- Types
  - bool
  - int in8 int16 int32 int64
  - uint uint8 uint16 uint32 uint64 uintptr
  - byte // alias for unit8
  - rune // alias for unit32 -> unicode code point
  - float32 float64
  - complex64 complex128 (made up of 2 floating point numbers, 2x float32 or 2x float64)
  - conversion is done with the expression `T(v)` - where T is any valid type
  - inference is done based on the value in the right hand side of the expression (even a function return)
- zero values:
  - 0 for numeric types
  - false for boolean
  - "" for strings
- Constants are declared using the `const` keyword
  - untyped constants are high precision
  - untyped constant will take the type needed by its context
- all integer types will over/underflow if you exceed their bounds

```
var x unit8 = 255 // range 0 - 255
x = x + 1 // result overflows and wraps around to 0

x = 4
x = x - 10 // result underflows and wraps around to 250
```

- floating point operations return `+Infinity or -Infinity`

### Functions

- a function can take 0+ arguments

```
func foo(x string, y bool) int {
  return 3;
}

foo(3, true)
```

- the type is declared after the variable name
- when 2 or more consecutive parameters share a type, you can omit all but the last type
  ` x int, y int, z int = x, y, z int`
- a function can return any number of results

```
func test....return y, x
a, b := test(param, param)`
_, b := foo() // discard variable a and extract b
```

- return values may be named
- a return statement without any values automatically returns the named return values in the function signature
  - only do this on short functions
- functions can be passed around like other values
  - they can be used as function arguments and return values
- functions can be closures, allowing the function to reference values outside its body
- Arguments are passed by value by default, they can also be passed by reference

```go
// Receives arguments as value
func swapVal(x, y int) int { }

// Receives arguments as reference
func swap(x, y *int) int { }

...
// call by reference
swap(&x, &y)

// call by value
swapVal(x, y)
```

### Flow control

- go only has one looping construct - for statement
- flow control blocks have their own scope, they do not share variables in the outer scope they are defined in
- `for <init>;<condition>;<post>`

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

  - the index or value can be skipped by using an underscore in its place, `_, value := range ....`

- if statement - () are optional, {} are needed
  - you can use shorthand statements in the condition `if v := math.Pow(x, n); v < lim {}`
  - variables declared in the statement, are available within the if and the else blocks
- Switch statement:
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

- a type switch can be used to switch based on the type of a value

```
switch v := i.(type) {
case T: ...
case S: ...
default: ...
}
```

- Defer - defers the execution of a function until the surrounding function returns
  - useful for functions that perform cleanup
  - pushed onto a LIFO stack
  - [defer](https://blog.golang.org/defer-panic-and-recover)
  - there are 3 rules that determine the behaviour of a defer
    - **A deferred function's arguments are evaluated when the defer statement is evaluated**
    - **Deferred function calls are a executed in LIFO after the surrounding function returns**
    - **Deferred functions may read and assign to the returning functions named return values**
      - this can be useful for modifying the error return value of a function
  - `recover` is used within deferred functions to "catch" errors
    - recover must be called directly in a deferred call
    - for the recover to execute it must be deferred before the panic occurs
    - by default a the function enclosing recover will return _0_ we can use **implicit** return to set the value returned by a recover

### Pointers

- Pointers hold the memory address of a value
- `var p *int` - p is a pointer to a int value, its zero value is `nil`
  - `*p` provides access to the pointer for read / write
- `&` generates a pointer to a variable, `p = &i`
- functions with a pointer argument must take a pointer
- methods with pointer receivers can take either a value or a pointer
  - go will automatically infer (&v) when you invoke a method that requires a pointer receiver

### Structs

- a collection of fields

```
type Vertex struct {
  X int
  Y int
}
```

- struct fields are accessed via the `.` operator
- a struct literal lets createa struct by listing the values of the fields
  - `v = Vertex{X: 1} // Y defaults to Y:0`
  - not all fields are required and order does not matter

### Arrays

- `var a [10]int` - a is an array of 10 integers
- arrays length are part of their type, so arrays can not be resized
- a `slice` is a dynamically sized, flexible view into the elements of an array
  - `[m:n]` extracts a slice from m until n, both are optional, m defaults to 0, n defaults to the length of the slice
  - slices are references to an array
  - slices dont store any data, they just describe a section of an underlying array
  - slice literals can be used to build an array create a slice to it
    - slice literals have no length
    - `[]bool{true, true, false}`
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

- maps keys to values
- the zero value is nil
- the make function is used to create map of a given type

```
type Vertex struct {
  ...
}
m = make(map[string]Vertex) // create a map of Vertex structs, with a string key
m["Bell Labs"] = Vertex { ... }
```

- map literals require the keys

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

- `delete(m, key)` - deletes the element at key `key` from map `m`
- `elem, ok = m[key]` - check if a key exists

### Methods

- a function defined on a type T, with a **receiver argument**
  - the receiver denotes the type the method applies to
  - the receiver appears between the func keyword and the method name
  - `func (v Vertex) Abs() float64 { ... }` - Abs method for type Vertex, return a float64
  - methods are functions
- methods can be defined on non-struct types

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

### Interfaces

- a set of method signatures
- a value of type interface, can hold any value that implements the set of methods
  - they can be thought of as a tuple of a value and a concrete type `(value, type)`
  - the concrete value can be nil
  - a nil interface has no value or concrete type, so causes a runtime error, as there is no type to indicate which concrete method to call
- interfaces are implemented implicitly
- `interface{}` is the empty interface
  - used to handle values of an unknown type such as `fmt.Print`
- type assertions provide access to the concrete value in an interface
  - `t := i.(T) // given interface i` - assert that i holds the concrete type T, assign T to the variable t
  - if it doenst a panic will occur
  - `t, ok := i.(T)` can be used to test whether an interface value holds a specific type

### Errors

- Error states are expressed with `error` values
  - `error` is a built in type interface

```
type error interface {
  Error() string
}
```

- errors can be handled by checking whether the error equals nil

### IO

- `io.Readers` interface represents a read stream of data
  - the interface has a read method `func (T) Read(b []byte) (n int, err error)`
  - read populates the given byte slice with data and returns the number of bytes populated and an error value
  - an `io.EOF` error is returned when the stream ends

### Images

- from package image, `type Image interface {}` defines an interface for images, with the methods
  - `ColorModel() color.Model`
  - `Bounds() Rectangle // note: this is a (image.Rectangle)`
  - `At(x, y int) color.Color`

### Concurrency

- **goroutines** are threads managed by the go runtime
- `go f(..)` evaluates the parameters in the current goroutine, but executes the function in a new goroutine
- goroutines run in the same address space, so access to memory needs synchronisation
- **channels** are a typed conduit for sending and receiving values
  - they use the `<-` operator
  - they are created using make `ch := make(chan int)`
  - sends and receives will block until the other side is ready

```
ch <- v // send v to channel ch
v := <-ch // receive data from ch and assign the value to v
```

- channels can be buffered, via a second argument to make `ch := make(chan int, 100)`
- sends will block when the buffer is _full_
- receives will block when the buffer is _empty_
- a sender can close the channel to indicate no more values be sent
- receivers take a second parameter `ok` to indicate if the channel is still open `v, ok := <-ch`
- `for i := range c` will receive values until the channel is closed
  - only **senders** should close a channel
  - close is only required when there are no more values coming
- `select` lets a goroutine wait on multiple operations
  - the `default` case can be used to try a send or receive without blocking

```
func f(c, quit chan int) {
  select {
    case c <- x:
      ...
    case <- quit:
      ...
    default:
      ...
    }
  }
}
```

- single direction channels can be created (receive/send only)

```
b := make(chan int)
var r chan<- int = b // receive only channel
var s <-chan int = b // send only channel
```

- `for <var> := range <channel> {}` is a short way to read from a channel until it closes

#### Links

- [Even in go, concurrency is hard](https://utcc.utoronto.ca/~cks/space/blog/programming/GoConcurrencyStillNotEasy)

## NLP

## Packages

### fmt

Format output

- **Stringer interface** - a type that can describe itself as a string
  - requires the `String() string` method to be implemented

### testing

Test framework

### Images

- [docs](chrome-extension://klbibkeccnjlkjkiokjodocebajanakg/suspended.html#ttl=The%20Go%20image%20package%20-%20The%20Go%20Blog&uri=https://blog.golang.org/go-image-package)

### time

time related functions

- Now() - UTC time

### math

Math libray

- rand
- Intn - return a number
- Seed - seed the number generator
- cmplx: complex numbers

### http

- `http.HandleFunc(resource, func (w http.ResponseWriter, r *http.Request) {})` | `http.Handle(requestHandler)` - handles any request sent to the specified resource
- `http.ListenAndServe(addr string, handler)` - listen on the address specified start serving
- `http.Handler(http.HandlerFunc)` - a type used to handle http requests, implements `http.ServeHTTP`
- `http.HandlerFunc(fn)` - an adapter to use ordinary functions as http handlers

## Glossary

- import - import go packages. By convention use the factored style `import ("fmt" "math" ...)`

### Useful links

- [Go blueprints - code for common tasks](https://yourbasic.org/golang/blueprint/)
- [Effective Go](https://golang.org/doc/effective_go.html)
- https://golang.org/doc/effective_go.html
- http://blog.golang.org/defer-panic-and-recover
- https://golang.org/src/encoding/json/example_test.go
- https://golang.org/pkg/fmt/
- https://golang.org/doc/articles/wiki/
- [Gobs of data](https://blog.golang.org/gobs-of-data)
- [Go web api example](https://github.com/caarlos0/go-web-api-example)
- [Go tooling workshop](https://github.com/campoy/go-tooling-workshop)
- [exercism - Learning tracks](https://exercism.io/tracks/go/learning)
  - [exercism - resources](https://exercism.io/tracks/go/resources)
- https://research.swtch.com/
- [Debugging simple memory leaks](https://medium.com/dm03514-tech-blog/sre-debugging-simple-memory-leaks-in-go-e0a9e6d63d4d)
- [Slice tricks - manipulating slices](https://github.com/golang/go/wiki/SliceTricks#reversing)
