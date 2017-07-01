# GO
* [Go spec](https://golang.org/ref/spec)

## General
* Every go program is made up of packages
  * By convention, the package name is the same as the last element of th eimport path -> math/rand files that being with package rand
  * when importing a package you can only refer to its exported names. Unexported names are private
* Programs start running in package `main`
* everything is pass by value (by default)
* must explicitly pass by reference ("&")
* public / private variables are declared by uppercase(first) / lowercase
  * a name that starts with an uppercase will be exported
* go routines - threads
* channels - communication and synchronisation between threads
* High level memory safe, garbage collected statically typed
* no classes or type inheritaance
  - ad hoc type relationships via interfaces
  - any type that implements all the methods of an interface, automatically implements the interface
  -


## Syntax
### General
* the var statement declares a list of variables, the type comes last
  - `var <variable> <type>`
  - initialisation can be used to infer a type, ie `var foo = "hello" <T = string>`
  ` var c, python, java bool`
  * it can include initializers, if so the type can be omitted
    `var i, j int = 1, 2`
    `var c, python, java = true, false, "no!"`
* `:=` can be used as a shorthand to declare a variable, type can be omitted
  - `x := 3`
  - we can also omit var
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
* Constants are declared using the const keyword
  - untyped constants are high precision
  - untyped constant will take the type needed by its context
* all integer types will over/underflow if you exceed their bounds
  -```
  var x unit8 = 255 // range 0 - 255
  x = x + 1 // result overflows and wraps around to 0

  x = 4
  x = x - 10 // result underflows and wraps around to 250
  ```
* floating point operations return `+Infinity or -Infinity`

### Functions
* a function can take 0+ arguments
  -```
  func foo(x string, y bool) int {
    return 3;
  }

  foo(3, true)
  ```
* the type is declared after the variable name
* when 2 or more consecutive parameters share a type, you can omit all but the last type
  ` x int, y int, z int = x, y, z int`
* a function can return any number of results
  ` func test....return y, x
    a, b := test(param, param)`
  - `_, b := foo() // discard variable a and extract b`
* return values may be named
* a return statement without any values automatically returns the named return values in the function signature
  - only do this on short functions

### Flow control
* go only has one looping construct - for statement
* flow control blocks have their own scope, they do not share variables in the outer scope they are defined in
* `for <init>;<condition>;<post>`
  - no braces around the statements
  - stops once the condition returns false
  - brackets are required
  - init, post are optional - `for sum < 1000 {}`
  - if you leave out the condition, you will have an infinite loop
* if statement - () are optional, {} are needed
  - you can use shorthand statements in the condition `if v := math.Pow(x, n); v < lim {}`
  - variables declared in the statement, are available within the if and the else blocks
* Switch statement:
  - case bodys break automatically unless it ends with a fallthrough statement
* Defer - defers the execution of a function until the surrounding function returns
  - pushed onto a LIFO stack
  - [defer](https://blog.golang.org/defer-panic-and-recover)

### Pointers

## Packages
### fmt
Format output

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
* https://golang.org/doc/effective_go.html
* http://blog.golang.org/defer-panic-and-recover
* https://golang.org/src/encoding/json/example_test.go
* https://golang.org/pkg/fmt/
* https://golang.org/doc/articles/wiki/
