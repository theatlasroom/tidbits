# Rust-lang
## Links
* [Official docs](https://doc.rust-lang.org)
* [Rust by example](http://rustbyexample.com)
* [Rust learning materials](https://github.com/ctjhoa/rust-learning)
* [Short exercises](https://github.com/carols10cents/rustlings)

## Quick overview
Created by mozilla to be safe, practical and low level

`rustc` is the rust compiler, it enforces safety and guarantees for your programs

By default, all variables are `immutable`, mutable variables need to be defined using `mut`

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
* use `let` to allocate space for a variable
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

## Detailed overview
### Introduction
* rust files have a .rs extension, the `rustc`  rust compiler can be used to generate a binary
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
* traits: a collection of methods, defined for an unknown type `Self`, they can access other methods declared in the same trait and can be implemented for any data type.
* macro: function calls that end with a `!`, these are expanded into source code and compiled with the program
