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
