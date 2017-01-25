# Python overview

## General
* Interpreted
* Whitespace dependent
* dictionaries and lists are mutable

## Keywords / functions
* print - print output to the screen
  - use a `,` to keep output on the same line
* datetime library is used to for datetime operations
  - datetime.now -> current timestamp
* raw_input() -> used to receive input from the user and waits for the enter key
* math module -> math operations
* can import whole modules or just a function
  - import math -> import math module, use functions like math.sqrt() (Generic import)
  - from math import sqrt -> import the sqrt function, now use it as sqrt()
  - from math import * -> import all the functions from the math module (Universal import)
* max -> return maximum of variable amount of arguments
* min -> return minimum of variable amount of arguments
* abs -> return absolute value of a number
* type -> return the type of the argument received
* del keyword to delete dictionary elements
* .remove to remove list items
* range has 3 types
  - range(stop)
  - range(start, stop) -> start at 0, stop at stop - 1 ie range(0,3) -> [0,1,2]
  - range(start, stop, step)
* zip -> create pairs for elements when passed 2 lists
  - it will stop at the shorter list
  - can handle more than 2 lists
* int() -> turn non-integer into an integer using base 10, optional 2nd parameter for base the number is in
* pass -> doesnt do anything, skip over areas of code that expect an expression (stub kind of thing)
* divmod returns a tuple containing the quotient and remainder divmod(177, 10) -> (17, 7  )
* pow(a,b) -> calculate a to the power of b. pow(a,b,m) -> a to the power of b, mod m
* sorted(iterable) -> takes any iterable and sorts it

## Magic variables
* `*args` and `**kwargs`
  - used in function defintions
  - allow you to pass a variable number of arguements to an function
  - `*args` -  variable non-keyworded arguements (normal argument list ie ('this','is', 'normal') )
  - `*kwargs` -  variable keyworded arguements (keyword based arguments ie (a='this',b='is', c='normal') )

## Syntax
* Comments with the # symbol
* """ (triple quotation marks) for multiline comments
* datatypes: int, float, boolean, strings, Lists
  - Strings can contain, number, characters or symbols
    - each character in a string has an index
    - slice a string using indexes string[start:end]
    - len, lower, upper and str are basic string functions
    - isalpha -> checks if the string only has a-z
    - `+` for string concatenation
    - `%` symbol after a string is used to replace the `%s` placeholders with a variable: print "Hello %s" % (name)
    - .split() -> split a string
  - Lists are like arrays
    - .index searches for a value, returns its index
    - .insert(index, item), insert item into position index
    - .sort() -> to sort the list
    - .pop(index) -> remove the item at the index and return it
    - .remove(item) -> remove the item from the list
    - del(list[index]) -> delete the item and the index but dont return it
    - list slicing list[start:end:stride] -> stride is the space between sliced items
    - slice indexes can be ommited and will use defaults ie [::2] -> start 0, end at end, jump by 2
    - -ve stride moves through the list from the last element to first
    - .filter(lambda, list) -> run a lambda function to filter the list
    - list.extend(L) -> merge another list onto the end
    - list.insert(i,x) -> insert element x at position i
    - list.count(x) -> count occurences of x
    - list.reverse()
  - Dictionary are like associative arrays (key value lookup)
    - .items() -> returns tuples of key value pairs in no particular order. A tuple is a immutable list, surrounded by `()`s
    - .keys() and .values() return arrays
* booleans can have the values **True** or **False**
* `**` symbol for exponentiation
* List comprehensions
  - evens_to_50 = [i for i in range(51) if i % 2 == 0] -> an array of items < from 0 to 50 that are even
* bitwise operations supported
  `
  print 5 >> 4  # Right Shift
  print 5 << 1  # Left Shift
  print 8 & 5   # Bitwise AND
  print 9 | 4   # Bitwise OR
  print 12 ^ 42 # Bitwise XOR
  print ~88     # Bitwise NOT
  `
* binary format numbers start with 0b -> 0b10 = 2, 0b101 = 5...
  - bin() -> return binary format of a integer, also oct() and hex()
* Tuple: similar to a list but is immutable
  - a = (2,6) -> define a tuple with 2 elements
  - used to simultaneously assign more than 1 variable in a statement
* Sets: unordered bag of unique values
  - initialized with set = {1,2} -> direct assigning values, set = set() -> initialize set, set = set([a,b,c]) -> create a set from a list
  - add(i) -> add item to the set
  - discard(v) -> remove the value from the set, do nothing if it doesnt exit
  - remove(v) -> remove the value from the set, raise an error if it doesnt exit
  - update(t) -> return the set with the items from t added, t must be iterable
  - a.union(b) -> return values in a or b
  - a.intersection(b) -> return values in a and b
  - a.difference(b) -> return values in a but not b

## Control flow
* 6 comparators `==` `!=` `<=` `>=` `<` `>`
* 3 boolean operators, and, not, or
  - order of operations: not -> and -> or
* elif instead of else if
* while / else and for / else
  - else executes if the loop condition evaluates to false -> if the while is never entered, or if the it exits normally. it wont execute on a break
* for index, item in enumerate(choices): -> supplies an index with each item in the list


## functions
* functions are first class -> can be used as variables or values
* 3 components
  - defintion done with the def keyword, followed by the name then parameters in paranthesis
  - optional comment describing the functions
  - function body  
* lambda x: x % 3 == 0 -> anonymous function that returns

## OO / Class basics
* class ClassName(object): -> define class ClassName that inherits from object
* __init__(self) -> constructor
  - self is a reference to the object being created
* override methods in subclasses by just defining them
* super(subclass, self).method() call parent class methods using the super command
* __repr__() -> representation, tells python how to represent an object of our class ie printing

## I/O
* open(file, permissions) -> open the file with relevant permissions
  - You can open files in write-only mode ("w"), read-only mode ("r"), read and write mode ("r+"), and append mode ("a", which adds any new data you write to the file to the end of the file).
* file.write(string) -> write string to the file
* file.read() -> read the whole file
* file.readline() -> read the file line by line
* file.close() -> must close the file to write to it properly
* read a file with ... as
  - `with open("text.txt", "w") as textfile:
	     textfile.write("Success!")`
  - this will automatically close the file at the end of the <blockquote></blockquote>
* check the .closed member to see if the file is closed or not

## Decorators
* Declared before function with the @ symbole
  - @api_view

## Notes
* IndentationError: expected an indented block - you should indent your code with 4 spaces

## useful links
* [Setting up virtualenvs](http://hackercodex.com/guide/python-development-environment-on-mac-osx/)
