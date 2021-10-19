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

## Parrallelism

* Go routines are [green threads](https://en.wikipedia.org/wiki/Green_threads) not OS threads
* The scheduler manages the low level interactions for threads
* Cheap to create and cheap to destroy
* `WaitGroups` can be used to synchronize threads

```go
...


// The main function acts as a go routine
// We have then spawned a second go routine within it
// We can use a wait group to enusre the program does not terminate until both are finished executing

func main() {
	var wg = sync.WaitGroup()
	var msg = "Hello"
	wg.Add(1) // Add a new thread to the wait group

	go func(msg string){
		fmt.Println(msg)
		wg.Done() // Decrement `1` from the waitgroup
	}(msg)

	// the waitgroup will complete when there are 0 items in it	
	wg.Wait() // wait for the waitgroups to complete their execution
}
```

* `WaitGroups` are safe to use concurrently
* `Mutex`s are locks that the application will honour
	* Can be useful to ensure only a singly entity can access a resource at a time
	* Simple mutex's only allow one entity to manipulate a resource at a time
	* `RWMutex` - multiple readers, but only one writer at a time. No writing while something is reading
	* `RLock`: Read lock
	* `Lock`: Write lock
	* We need to ensure we lock the mutex outside the context of the goroutine that relies on it

```go
// This example forces sequential execution, so this usually isnt a good idea
var m = sync.RWMutex()
counter := 1

func main() {
	for i := 0; i < 10; i++ {
		wg.Add(2)
		m.RLock()
		go doWork()
		m.Lock()
		go increment()
	}
	wg.Wait()
}

func doWork() {
	fmt.Printf("Hello #%v\n", counter)
	m.RUnlock()
	wg.Done()
}

func increment(){
	counter++
	m.Unlock()
	wg.Done()
}
```

* By default go can provide the same number of threads as there are OS cores
	* `runtime.GOMAXPROCS(int)` can be called to use more / less threads
	* A negative number will just return the number of threads available

```go
func main() {
	runtime.GOMAXPROCS(-1) // returns the number of threads available
}
```
* Don't create concurrency within a library
	* It's better for consumers to manage concurrency on their own
	* Exposing channels can be a better option if you really need concurrency
* When you create a goroutine, make sure to know how it will stop
* Use the race flag to check for data races `go <run|build|install> -race`
* `Channels` are used to synchronize data between goroutines
	* channels are created with `make`
	* channels are strongly typed
	* data is passed by copy
* Dedicated read/write channels are preferable
	* `ch <- chan int` read only channel (receive)
	* `ch chan<- int` write only channel (send)
	* `ch chan int` read/write channel
	* Channels will be cast to the correct type (read/write/both) when passed to a function
* Unbuffered channels only allow one message at a time
  * pushing data onto a channel is blocking
	* deadlock (all goroutines are asleep) can occur when we attempt to push data to a channel and there is no receiver

```go

// the channel arrow points in the direction the data should go into 
// `i <- ch` read from channel
// `ch <- 42` write to channel
var wg = sync.WaitGroup()

func main(){
	ch := nmake(chan int) // create an int channel
	wg.Add(2)

	go func(){
		i := <- ch // receive a value 
		fmt.Println(i)
		wg.Done()
	}()

	go func(){
		ch <- 42 // send 42 to the channel
		wg.Done()
	}()

	wg.Wait()
}
```

* Buffered channels are useful for asymmetrical read/writes
	* useful when the sender / receiver move data at different rates
	* closing the channel will signal there's no more data `close(ch)`
	* writing to a closed channel will panic

```go
ch := make(chan int, 50) // create a buffered channel, it can hold 50 items

// iterate over the messages in the channel
for i := range ch {
	fmt.Println(i)
}
```
* An application shuts down after the final statemment in the `main` function is executed
	* goroutines that are still executing will end abruptly
	* always ensure you have a way to close your goroutine when you declare it
* Signal only channels are useful for indicating when a channel can be closed
	* a struct with no fields allocates 0 memory
	* a channel `select` statement with no `default` option will block
```go
var logCh = make(chan logEntry, 50) // buffered channel for log messages
var doneCh = make(chan struct{}) // cant send any data, only a signal that a message was sent

func main(){
	go logger()
	logCh <- logEntry(time.Now(), logInfo, "App is starting")
	logCh <- logEntry(time.Now(), logInfo, "App is shutting down")
	time.Sleep(100 * time.Millisecond)
	doneCh <- struct{}{} // define and initialize an empty struct, signal to the chanel we are done
}

func logger() { 
	for {
		// the select statement blocks until a message is received on one of the channels
		select {
		case entry := <-logCh:
			// do stuff
		case <- doneCh:
			// break out of the infinite loop when we are done
			break
		}
	}
}

func nonBlockingLogger() { 
	for {
		select {
		case entry := <-logCh:
			// do stuff
		case <- doneCh:
			// break out of the infinite loop when we are done
			break
		default: // adding `default` makes the select Non-blocking
		}
	}
}
```
## Testing
