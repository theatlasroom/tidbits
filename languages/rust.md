# Rust-lang
## Links
* [Official docs](https://doc.rust-lang.org)
* [Rust by example](http://rustbyexample.com)
* [Rust learning materials](https://github.com/ctjhoa/rust-learning)
* [Short exercises](https://github.com/carols10cents/rustlings)

## Quick overview
Created by mozilla to be safe, practical and low level

**rustc** is the rust compiler, it enforces safety and guarantees for your programs

By default, all variables are **immutable**, mutable variables need to be defined using **mut**

blocks can be defined using the `{ }`

### Primitive data types
* integer 8, 16, 32, 64: i8, i16....
* unsigned integer 8, 16, 32, 64: u8, u16....
* float 32, 64: f32, f64
* integer based on the buffer size of your machine: isize, usize
* bool: boolean
* char: individual character

### Syntax overview
* fn is used to define a function
* use **let** to allocate space for a variable
  - can define multiple variables in one line ie `let (fname, lname) = ("Some", "Person");`
* use '{}' for print formatting => `println!("I am {} years old", age);`
  - can use `{0}, {1}`... to select a specifc output variable
  - `{:.2}` => 2 decimal places
  - `{:b}` - binary, `{:x}` - hexadecimal, `{:o}` - octal
  - named arguments can be used `println!("{ten:>ws$}", ten=10, ws=5);`
* range: <num>..<num>
* loop:
  `loop {
    if (x < 10){
      println!("{}", x);
      x += 1;

      continue;
    }
    else {
      break;
    }
    x++;
    continue;
  }`
  - loops can be named
    `'outer: loop { }`
* while: `while<condition>{}`
* for: `for<condition>{}`
* match: similar to a switch statement in other languages
  `match text {
      Some(x) => println!("{}", x),
      Some(y) => println!("{}", y),
      None => break,
  }`
* vectors: variable sized arrays `let v = vec![1,2,3,4,5];`
  - supports push and pop operations
* tuples: fixed length key value pairs `let t = ("age", 40);`
  - you can define the types supported `let ts: (&str, &i32) = ("age", 10);`
* closures: blocks of code that can accept paramters and can also be passed to other functions
  - `let sum_nums = |x: i32, y: i32| x + y; println!("7 + 8 = {}", sum_nums(7,8))`
  - can access variables defined outside of the function
* structs are used to create custom data types

## Cargo
Cargo is rust's build and package management system
* builds your code
* downloading dependencies
* building dependencies
* should come bundled with rust
* expects your source code to be in a *./src* dir
* any .rs files in your *./src/bin* directory will be compiled into individual binaries
* outputs builds to *./target* dir
* use [TOML](https://github.com/toml-lang/toml) config files to specify configurations for the project - *the file must be named Cargo.toml*
* **cargo build** builds the project
* **cargo run** builds and runs the project
  - `--bin` flag used to specify the binary to run (if we have files in the bin directory)
* **cargo build  --release** compiles the project with optimizations
* the *Cargo.lock* file is created to track your dependencies
* **cargo new** creates a new project, use the --bin flag for binaries, otherwise it defaults to a library

### Notes
* [Overview of Cargo.toml](http://doc.crates.io/manifest.html)

## Syntax
### variables
* `let` is used to bind some value to a name
* the left hand side of a let statement is a **pattern**, not a variable name
* rust is *statically typed*, types a specified and checked at compile time, rust also supports *type inference*
* types can be specified with a colon `let x: i32 = 5; // create a binding *x* of type 32bit signed integer, and value 5`
  - *i* - signed integers
  - *u* - unsigned integers
  - sizes can be specified as 8, 16, 32 and 64 bit
* bindings are *immutable* by default and will throw a compiler error
* *mut* can be used to make a *mutable* binding ie `let mut x = 5; x = 10;`
* bindings are required to be initialized before they can be used, or they will throw a compiler error
* bindings have a scope constrained to the block they were defined in
* *shadowing* - allows rebinding a name to a value of a different type, or change the mutability of a binding

### functions
* every program has a main function
* functions have the syntax `fn function_name(arguments) -> return_type { expressions ... }`
* arguments are seperated by a comma
* argument types must be specified
* the last line of a function is its return value
* *return* can be used for an early return from the function
  - it is poor style to use return at the end of a function, instead omit the last semi-colon
* *diverging functions* are functions that do not return a value
* variable bindings can point to functions `let f: fn(i32) -> i32;`

### Primitive types
* `bool`: boolean value
* `char`: 4 byte unicode scalar value
* numeric data can be a combination of
  - signed / unsigned
    * signed numbers use twos complement
  - integer, float
  - 8,16,32,64 bit
  - `i8`, `u32`, `f64` etc
  - `isize` and `usize` are pointer sized int/unsigned ints
* Arrays have type `[T; N]` - N is the compile time constant for the length of the array
  - each element can be initialized to the same value `let a = [0; 20];`
  - `.len()` returns the number of elements in the array
  - Slices can be used to extract a subset from a referenced array
    `let a = [0,1,2,3,4]; // define an array
     let middle = &a[1..4]; // slice the values 1,2,3 from the array a`
  - `str` is the primitive string
* Tuples - ordered list of fixed sized `let x = (1, "hello"); // tuple  i32, &str`
  - one tuple can be assigned into another if they have the same contained types and length
  - fields of a tuple can be destructured `let (x,y,z) = (1,2,3);`
  - fields can also be accessed with an index
    `let tuple = (1,2,3);
     let x = tuple.0;`
* functions have a type, it specifies what can be returned
  - `fn simple(x: i32) -> i32 { x }`
  - `fn complex(x: i32) -> (i32, i32) { (10, 10) }`

### Comments
* line comments `//`
* doc comments `///`
  - supports the use of markdown within
  - it is a good idea to provide examples of usage
* the `//!` syntax of doc comment is used inside crates, modules or functions
  - used to comment containing items
* use the `rustdoc` tool to generate HTML documentation from doc comments and run the code examples

### If / Loops
* If syntax `if <expression> { ... } else if <expression> {} else { ... }`
  - if is an expression
  - if will return the value of the last expression from the branch that is chosen
* conditional binding `let y = if x == 5 { 10 } else { 15 }`
* rust provides 3 kinds of iterative acitivies, loop, while and for
* `loop`: infinite loop
  - a way to loop indefinetly until a terminating statement is reached
  - `loop { println!("Keep on keeping on"); }`
* `while`: loop until a condition is met
   - `while <expression> { ... }`
* `for`: used to loop a specific number of times
  - `for <variable> in <expression> { ... }`
  - the <expression> must be an item that can be converted into an iterator
  - the iterator returns a series of element, one for each iteration of the loop
  - the value of the current iteration is bound to <variable>, which is valid in the loop body
  - rust does not have c-style for
  - `<expression>.enumerate()` keeps track of the current index
    * `for (index, value) in (5..10).enumerate() { ... }`
* `break;`: break a looping structure early  
* `continue;`: break the current iteration and move onto the next one
* nested loops can be given labels
  `'outer': for x in 0..10 {
      'inner': for y in 0..10 {
        if x % 2 == 0 { continue 'outer'; }
        if y % 2 == 0 { continue 'inner'; }
      }
  }`

### Vectors
* dynamic array allocated on the heap, implemented as `Vec<T>`
* `let v = vec![1,2,3,4,5]; // v: Vec<i32>`
* `let v = vec![0; 10]; // vector of ten zeros`
* the size of type T must be known at compile time
  - if you wont know the size, use a Box
* an item from the vector can be retrieved via its index
  - index must be a `usize`
  - `v[3]; // returns the 4th element in the vector`
* accessing an index that doesnt exist will result in a `panic`
* use `.get(index)` or `.get_mut(index)` to access an index without panic-ing
  - returns `None` when given an invalid index
* you can iterate over a vector with a `for`
  - `for i in &v { ... } // iterate over a reference to v`
  - `for i in &mut v { ... } // iterate over a mutable reference to v`
  - `for i in v { ... } // take ownership`
  - if you take ownership, you cannot use the vector again

## std - Standard library
### std::fmt
* utilities for formatting and printing Strings
* `format!` - macro for runtime formatting of arguments into strings
  - the `{}` curly braces specify a placeholder that can be substituted for a argument, by default arguments are passed as comma separated values after the string
  - the `{n}` syntax specifies to use argument at index `n` in this position
  - a compile time error is throw if a format string doesnt use all its arguments
  - this macro supports named parameters `format!("Hello {name}", name="Jon"); // prints "Hello Jon"`
  - a type can be specified by supplying it within the curly braces
    * no type => `Display`
    * ? => `Debug`
    * o => octal
    * x => LowerHex
    * X => UpperHex
    * p => pointer
    * b => Binary
    * e => LowerExp
    * E => UpperExp

### std::iter
* IntoIterator
  - a trait used to define how a type will be converted to an iterator
  - allows your type to work with rust's for loop syntax
  - `impl IntoIterator for <collection> { ... }`

### std::vec
A contiguous growable array with heap allocated contents
vectors have O(1) indexing, push and pop
* vecs are a *LIFO* stack (last in first out)
* `let v: Vec<i32> = Vec::new();` or `let v: Vec<i32> = vec![];`
* `.push(item)`: push values onto the end
* `.pop()`: return the last element in the vector

### Notes
* the [prelude](https://doc.rust-lang.org/std/prelude/) contains the default set of code that is imported into every program
* Associated functions have the form `<Type>::function()` aka static method
* `panic!` exits the program
* **Result** types are used to encode error handling information
  - the expect method checks the value of the response and will call `panic!` if it doesnt match

## Rust by example
### Introduction
* rust files have a .rs extension, the **rustc**  rust compiler can be used to generate a binary
* Regular comments use `//`, multiline/block comments use `/* */`, Doc comments for the following item use `///` and `//!` generates library docs for the enclosing item
* `std::fmt` defines macros for printing
  - `format!`: write formatted text to String, `print!` same as format! but prints to the console and `println!` same as print! but adds a new line
  - `println!("{0}", "Cool")`
  - use `{:>SOMEVALUE$}` to specify whitespace to pad the output with
  - `std::fmt::Debug` uses the `{:?}` marker to format text for debugging
  - `std::fmt::Display` uses `{}` marker to format text

## Notes
* Anything with an exclamation mark at the end is a macro
* rust error messages can be put into the compiler to be given a full explanation of the error
* `chars()` returns an iterator

## Glossary
* traits: a collection of methods, defined for an unknown type **Self**, they can access other methods declared in the same trait and can be implemented for any data type.
* macro: function calls that end with a `!`, these are expanded into source code and compiled with the program
