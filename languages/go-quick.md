# Go quick

A collection of short tidbits / useful things in go

## /b/

* the `t.(type)` operation returns the type of our variablet
## Variables

* Variables can't be declared twice in the same scope

```go
var i int = 10	

func main() {
	var i int = 42 // valid redeclaration at this point
	var i int = 10 // invalid - no new variables on the left hand side
	i = 10 // valid reassignment of the value
```

* shadowing: variables take the **innermost** value assigned to them

```go
var i int = 10

func main() {
	fmt.Println(i) // outputs 10
	var i int = 42 
	fmt.Println(i) // outputs 42
}
```

* Dump the type and value of a variable

```go
i := 10
fmt.Printf("%v, %T", i, i) // prints out the value and type of the variable
```

* Lowercase variables are always scoped to the package
* Uppercase variables at the package level are exported and globally available
* Everytime you initialize a variable it has a 0 value

## Constants

* Constants have to be assignable at **compile time**, they cant be to set to values that need to be resolved at run time, such as:
	- command line flags
	- result of a function
* Collection types cannot be contants
* Constants follow the same shadowing rules as variables
* The compiler replaces constants with their literal value, so implicit conversions can occur

```go
func main() {
	const a = 42  // int
	var b int16 = 27
	// the next line is valid, because the a will be replaced with it's literal value 42
	fmt.Printf("%v, %T", a + b, a + b)  // returns 69, int16
}
```

* Non - zero enumerated constant

```go
const (
	_ = iota
	one
	two = iota + 2
	three
)

func main() {
	fmt.Printf("%v, %v, %v", one, two, three) // 1, 4, 5
}

```

* File size constants

```go
const (
	_ = iota
	KB = 1 << (10 * iota)
	MB
	GB
	TB
	PB
	EB
	ZB
	YB
)

func main(){
	fileSize := 4000000000.
	fmt.Printf("%.2fGB", fileSize/GB)
}
```


## Logic

* Multiple conditions can be used in each switch test case

```go
switch 4 {
	case 1, 5, 10:
		...
	case 2, 4, 6:
		...
	default: 
		...
	}
}
```

* Switch statements can branch on an expression

```go
num := 0
switch i := num % 2; i {
  case 1: 
    fmt.Println("That's odd!")
  default:
    fmt.Println("Even steven")    
}
```

* Tagless switch

```go
i := 0
switch {
  case i % 2 == 1: 
    fmt.Println("That's odd!")
  default:
    fmt.Println("Even steven")    
}
```

* Type switching can be used

```go
var i interface{} = 1
switch i.(type) {
	case int:
		...
	case float64:
		...
	case string:
		...
	default:
		...
}
```

* Increment 2 variables in a for loop

```go
// Note: we can't use the `++` syntax to increment as its an statement
// the increment section (final part of for loop declaration) can only take a single statement, not multiple statements
for i, j, := 0, 0; i < 5; i, j = i+1, j+1 {
	fmt.Println(i,j)
}
```

* Labelled loops allow complex control over `break` statements
```go
Loop:
	for i := 1; i <= 3; i++ {
		for j := 1; j <= 3; j++ {
			fmt.Println(i*j)
			if i * j >= 3 {
				break Loop
			}
		} 
	}
}
```

* Defer statements take the arguments at the time the `defer` is called

```go
func main() {
 a := "start"
 defer fmt.Println(a)
 a = "end"
}

// prints "start"
```

## Memory, structs, pointers and interfaces
* the asterix `*` operator can be used to
	- _Create a pointer_ to a variable of type T `var b *int`
	- _Dereference_ the value of a pointer `fmt.Println(*b)`
* pointer arithmetic is not allowed outside of the [unsafe](https://pkg.go.dev/unsafe) package
* Uninitialized pointers take the `nil` value
* the dereference `*` operator has a lower precedence than the `.` operator

```go
...
var ms *myStruct
ms = new(myStruct)
(*ms).foo = 42 // dereference `ms`
*ms.foo = 42 // dereference `ms.foo` object
// A sneaky point to note
ms.foo = 42 // Here the compiler will still correctly dereference `ms`
```

* functions can safely return a pointer, the compiler move the value to the heap

```go
func sum(...) *int {
	var result *int
	...
	return &result
}
```

* By convention single method interfaces should be named after the method + `er`

```go
type Writer interface {
	Write([]bytes) int
}
```

* Variables declared using a concrete type only have access to the value receiver methods, pointer variables have access to all pointer receiver methods and value receiver methods

```go
type WriterCloser interface {
	Write([]byte) (int, error)
	Close() int
}

type myWriter struct {}

func (mw *myWriter) Write(data []byte) (int, error) { ... }
func (mw myWriter) Close() int { ... }

func main() {
	mwConcrete := myWriter{} // Can only access Close, no access to Write
	mwPointer := &myWriter{} // Can access Write and Close
}
```

* Prefer many, small interfaces over any large ones
* Prefer to export a concrete type instead of interfaces, this will simplify mocking for tests
	* Don't assume you know how consumers will use your type
* If you're pulling in a value, accept an interface instead of a concrete type
* Design functions and methods to receive interfaces wherever possible