# Go quick

A collection of short tidbits / useful things in go

## /b/

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

* dump the type and value of a variable
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
