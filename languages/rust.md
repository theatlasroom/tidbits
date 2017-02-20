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
  - can define multiple variables in one line ie
```
let (fname, lname) = ("Some", "Person");
```
* use '{}' for print formatting => `println!("I am {} years old", age);`
  - can use `{0}, {1}`... to select a specifc output variable
  - `{:.2}` => 2 decimal places
  - `{:b}` - binary, `{:x}` - hexadecimal, `{:o}` - octal
  - named arguments can be used `println!("{ten:>ws$}", ten=10, ws=5);`
* range: <num>..<num>
* loop:
```
loop {
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
}
```
  - loops can be named
    `'outer: loop { }`
* while: `while<condition>{}`
* for: `for<condition>{}`
* match: similar to a switch statement in other languages
```
match text {
    Some(x) => println!("{}", x),
    Some(y) => println!("{}", y),
    None => break,
}
```
* vectors: variable sized arrays `let v = vec![1,2,3,4,5];`
  - supports push and pop operations
* tuples: fixed length key value pairs `let t = ("age", 40);`
  - you can define the types supported `let ts: (&str, &i32) = ("age", 10);`
* closures: blocks of code that can accept paramters and can also be passed to other functions
```
let sum_nums = |x: i32, y: i32| x + y; println!("7 + 8 = {}", sum_nums(7,8))
```
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
```
let a = [0,1,2,3,4]; // define an array
let middle = &a[1..4]; // slice the values 1,2,3 from the array a
```
  - `str` is the primitive string
* Tuples - ordered list of fixed sized `let x = (1, "hello"); // tuple  i32, &str`
  - one tuple can be assigned into another if they have the same contained types and length
  - fields of a tuple can be destructured `let (x,y,z) = (1,2,3);`
  - fields can also be accessed with an index
```
let tuple = (1,2,3);
let x = tuple.0;
```
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
```
'outer': for x in 0..10 {
    'inner': for y in 0..10 {
      if x % 2 == 0 { continue 'outer'; }
      if y % 2 == 0 { continue 'inner'; }
    }
}
```

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

### Ownership
* variable bindings have *ownership* of what they are bound to, so when they go out of scope, rust will free their bound resources
* rust ensures there is **exactly one** binding to any given resource
* `error use of moved value` - occurs when we try to access a old binding on a resource that has been assigned to another binding
```
let v = vec![1,2,3];
let v2 = v;
// we can no longer access v
// the resource v was bound to has 'moved'
  ```
* the `Copy` trait will copy the contents of a binding when we assign a new binding to it, but will allow us to still use the original binding
  - this trait means that the binding does not get moved
  - all primitives implement this trait

### Borrowing
* Borrowing allows us to use a binding in another scope, but keep control of the binding after the scope is removed
* by using a reference, we allow the new scope to borrow the binding
* a scope that borrows a binding does not deallocate the binding when it goes out of scope
```
let v1 = vec![1,2,3];
let v2 = vec![4,5,6];

fn foo(v1: &Vec<i32>, v2: &Vec<i32>) -> i32 {
  v1[0] + v2[0]
}

foo(&v1, &v2);
// we can still use v1/v2 after this
```
* borrows are immutable by default and will need to be specified as mutable
  ```
  let mut x = 5;
  {
    let y = &mut x;
    *y += 1;
  }
  println!("{}", x);
  ```
    - the `*` allows us to access the contents of the mutable reference `y`
* any borrow must last for a scope no greater than that of the ownership
* you can only have one of the following occurences:
  - **one or more** references (&T) to a resource
  - **exactly** one mutable reference (&mut T)

### Lifetimes
* solve problems with borrowing references someone else owns
* `'<var>` is used to control the lifetime of a binding
  - `fn skip_prefix<'a, 'b>(line: &'a str, prefix: &'b str) -> &'a str { .. }`
  - the function above specifies 2 lifetimes 'a and 'b
  - each reference in the function signature is associated with one of the lifetimes
  - the reference line, uses lifetime 'a which is part of the return type, so the compiler knows not to deallocate line at the end of the function call
  - str can be safely deallocated as its lifetime does not extend past the scope of the function
* lifetimes can usually be omitted except for when the compiler explicitly requires them in complex situations
* lifetimes are a type of generic
* `&'a mut i32` - a mutable reference to a binding with a lifetime 'a
* multiple references can use the same lifetime
* `'static` defines a lifetime for the whole program

### Mutability
* everything is immutable by default
* `mut` allows us to define a binding as mutable
  - this means you can change what the binding points to
   ```
   let mut x = 7;
   x = 10;
   ```
* `&mut` allows us to define a mutable reference
  ```
  let mut x = 5;
  let y = &mut x;
  ```
* exterior mutable - types that can be mutated outside of themselves ie by cloning the data
* interior mutable - types that can return mutable references to their data
* the mutability of struct is in its binding
  - they do not allow mutability at the field level

### Structs
* used to create complex data types
* `struct <MyStructName> { field: type,... }`
* to use a struct we can create an instance of it, passing a list of key value pairs to set the fields
  - `let s = MyStructName { field: value, ... }`
  - instances are immutable by default, but can be bound with `mut`, this will allow us to mutate fields in the struct
* fields can be accessed using `.` dot notation
  - fields can be mutable pointers
  - `struct PointRef<'a> { x: &'a mut i32, y: &'a mut i32 }`
* `..` can be used to copy values from a similar struct
  - `struct Point3d { x: i32, y: i32, z: i32 };
    let mut point = Point3d { x:0, y:0, z:0 };
    point = Point3d { y:1, ..point }; // the x and z values will be copied into this new point`
* tuple structs are defined with a name but no fields, just a tuple
  - `struct Color(i32, i32, i32);`
  - members can be accessed with a destructuring pattern, or by index
    ```
    let col = Color(0,0,0);
    let Color(red, _, blue) = col;
    let green = col.1;
    ```
* the *newtype pattern* defines a tuple struct with a single value
  - `struct Inches(i32)`
  - the new type is distinct from its contained value
* the *unit struct* is an empty struct
  - useful when you need to create a structure to implement a trait, but dont need to worry about storing data

### Enums
* represents data that is one of several possible variants, each of which may have data associated with it
* syntax is similar to structs, enums can be
  - unit enums (no data)
  - enums with named data
  - enums with unmaed data (similar to tuple structs)
* unlike structs, an enum is a single type
* a value of the enum can match any of the variants
* use `<enum-name>::<variant-name>` to access a variant of the enum
  - each variant is scoped to the enum they are part of
* an enum constructor can be used like a function
```
enum Message {
  Move(x: i32, y: i32),
  Write(string),
}

let m = Message::Write("Hello, world".to_string());
```

### Match
* used to replace complicated `if/else` groups
* useful when you have more than 2 possible options in place of an if/else or with complex conditions
```
let dice_roll = 50;
match dice_roll {
  1 => println!("Rolled a 1"),
  2 => println!("Rolled a 2"),
  3 => println!("Rolled a 3"),
  4 => println!("Rolled a 4"),
  5 => println!("Rolled a 5"),
  6 => println!("Rolled a 6"),
  _ => println!("That is not a valid dice roll m8"),
}
```
* match is an implementation of pattern matching
* match enforces `exhaustiveness checking` to ensure we check all possible values for the type we are using
  - the `_` underscore will catch any value we have not defined an expression for
* match is an expression so we can use `let number = match x { ... }` to bind the result of a match
* we can also match on enums
```
enum Meal {
  Breakfast,
  Lunch { location: String, time: i64 },
  Dinner(location: String, time: i64, address: String),
  Snack(String),
}

fn  eat_breakfast(){ ... };
fn  eat_lunch(location: String){ ... };
fn  eat_dinner(){ ... };
fn  eat_snack(snack_type: String){ ... };

fn pick_a_meal(meal: Meal){
  match meal {
     Meal::Breakfast => eat_breakfast(),
     Meal::Lunch { location: some_location, time: some_time } => eat_lunch(),
     Meal::Dinner(some_location, some_time, some_address) => eat_dinner(),
     Meal::Snack(some_snack) => eat_snack(),
  }
}
```

### Patterns
* patterns are used in variable bindings, match expressions and other areas
* patterns can have a side effect of shadowing (a variable in a inner scope having the same name as one in an outer scope), this will cause the variable in the inner scope to overwrite the value of the same variable in the outer scope
* `|` can be used to match multiple patterns
```
let x = 1;
match x {
  1 | 2 => println!("one or two"),
  _ =< println!("anything else"),
}
```
* compound data types like structs, tuples and enums can be *destructured* inside a pattern
```
struct Point { x: i32, y: i32 };
let origin = Point { x: 0, y: 0 };
match origin {
  Point { x, y } => println!("{},{}", x, y),
}
```
* the `:` symbol can be used to change the name of a value
```
match origin {
  Point { x: x1, y: y1 } => println!("{},{}", x1, y1),
}
```
* the `..` symbol will allow us to ignore values we dont need
```
match origin {
  Point { x, .. } => println!("{},{}", x), // ignore the y binding
}
```

* the `_` underscore and be used to ignore the type and value of a pattern
```
// For Result<T, E>
match something {
  Ok(value) => println!("{} is our value", value),
  Err(_) => println!("we have an error"),
}
```
  - you can also ignore parts of any type of structure
```
fn coordinate() -> (i32, i32, i32) { ... } // returns a tuple with 3 values
let (x, _, z) = coordinate()
```
    * in this case, the value never gets bound, so it does not *move*
* the `..` can also be used to ignore multiple values
```
enum OptionalTuple {
  Value(i32, i32, i32),  
  Missing,
}

let x = OptionalTuple::Value(1,2,3);
match x {
  OptionalTuple::Value(..) => println!("We got a tuple"),
  _ => println!("No luck"),
}
```
* `ref` and `ref mut` can be used to create a reference for us in the pattern
```
let mut x = 5;
match x {
  ref mut mr => println!("mutable reference to {}", mr),
}
```
* you can match a range of values with `...`
  - mostly used with integers and chars
````
match number {
  1 ... 5 => println!("one - five")
  ...
}

match letter {
  'a' ... 'j' => println!("a - j"),
  'k' ... 'z' => println!("k - z"),
  ...
}
````

* `@` can be used to bind values to names
```
match x {
  e @ 1 ... 5 => println!("got a range element {}", e),
  ...
}
```
* `guards` can be used to add conditions to matchs
```
match x {
  OptionalInt::Value(i) if i > 5 => println!("Bigger than 5")
  ...
}
```

### Method syntax
* rust provides a mechanism to use *method call syntax*, allowing us to chain function calls
```
foo.bar().baz()
```
* the *impl* keyword allows us to define methods
* the first parameter of a method can be `self`, `&self` or `&mut self`
* we should default to `&self` so that we only borrow self, and dont take ownership or create a mutable reference if we do not need to

```
struct Circle {
    x: f64,
    y: f64,
    radius: f64,
}

impl Circle {
    fn area(&self) {
       println!("taking self by reference!");
    }

    fn radius(&mut self) {
       println!("taking self by mutable reference!");
    }

    fn circumference(self) {
       println!("taking ownership of self!");
    }
}
```
* if our return type matches the type of self, we can chain the methods
* *Associated functions* can be defined for a type, but do not take self as an arguement. Analogous to static class methods in that they dont require an instance of the type.

* Rust doesnt have method overloading, named arguments or variable arguments, so we can use the *builder pattern* instead to construct instances of a type

### Strings
* in rust a string is a sequence of unicode scalar values, encoded as a stream of UTF-8 bytes
  - all strings are guaranteed to a be a valid encoding of UTF8 sequeces
  - strings are not NUL terminated (\0) and can contain NUL bytes
* there are 2 types of strings:
  - `&str` string slices, an immutable fixed size string that is a reference to a sequence of UTF8 bytes
    * a string literal is a slice that is statically allocated
    * any function that accepts string slices can accept a string literal
    * str is an unsized type
  - `String` a heap allocated string, they can be created by converting from a slice using the `to_string` method
    * only a &str can be concatenated onto a String
    * `push_str()` can be used to concatenate a string
    * Strings will coerece into a slice with a &
* Strings do not support indexing
  - `.chars().nth(index)` can be used to get a result similar to an index
* Strings can be sliced with slicing syntax, the indexes are byte offsets not characters (a character can be composed of multiple bytes)

```
let name = "bob loblaw"; // &'static str
let mut lawyer = name.to_string();
let mut prefix = "Dr.".to_string();
let first = &name[0..4];

let final_name = prefix + &lawyer; // use &str when concatenating to Strings
```

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

### std::env
* `args` - returns the arguments passed into the program

### std::fs
Filesystem io
#### Structs
* `DirBuilder` - used to create directories
* `DirEntry` - entries returned from the ReadDir iterator
* `File` - reference to an open file on the Filesystem
* `FileType` - represents a tpye of file, with accessors for each file type
* `Metadata` - metadata about a fiel
* `OpenOptions` - options and flags to configure how a file is opened
* `Permissions` - Representation of the various permissions on a file
* `ReadDir` - Iterator over the entries in a directory

#### Functions
* `canonicalize` - returns the canonical form a of a path
* `copy` - copy the contents of one file, including the permission bits
* `create_dir` - create a new empty directory
* `create_dir_all` - recursively create a directory and all its components
* `hard_link` - create a new hard link on the filesystem
* `metadata` - given a path, query the filesystem to get information about a file, directory etc
* `read_dir` - returns an iterator over the entries in a dir
* `read_link` - read a symbolic link and return the file it points to
* `remove_dir` - remove an existing, empty dir
* `remove_dir_all` - recursively remove an existing, empty dir
* `rename` - rename a file or dir
* `set_permissions` - changes the permissions found on a file or a directory
* `symlink_metadata` - query metadata about a file, without following the symlinks

### std::io
#### Structs
* `Stdin` -

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

## General Notes
* [Rust + node](https://blog.risingstack.com/how-to-use-rust-with-node-when-performance-matters/)
