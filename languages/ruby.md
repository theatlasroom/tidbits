# Ruby
## General

- High level, _interpreted_, _oo_
- Developed by Yukihiro Matsumoto (Matz)
- Everything is an object
  - Methods have implicit return, returing the last evaluated expression in a method body 
- local variables should lowercase with `snake_casing`
- `method!` methods mutate their caller
- `method?` methods return true / false
- ranges are defined by `...` or `..`
  - `..`: inclusive
  - `...`: exclusive
- `loop` can be used to repeatedly execute a block
  - `break` is used to exit a loop
  - `next` can be used to skip the current value in a loop or for
- blocks can be defined using `do` and `end` or `{}`
- Hashes can be defined in two ways: 
- Arguements are when calling a method, parameters are in the definition
  - Parantheses are mostly optional
  - `Splat` arguments are preceeded by a _*_, used for methods that can receive multiple arguments
- _Blocks_ are similar to anonymous functions
  - can be passed to methods as parameters
  - useful for defining a method at the point it is called
- `<=>` combined comparision operator takes 2 parameters and returns -1, 0, 1 with the same logic used in `.sort`
- `false` and `nil` are the only non-true values
  - `false`: !true
  - `nil`: nothing
- `:symbols` can be used as keys for hashes
  - Only 1 copy of any particular symbol exists at any time
  - They can be used as hash keys or for referencing method names
  - Immutable and perform better than strings as keys
- `||=` conditional assignment, assigns a variable only if it doenst already have a value
- `<<` concatenates the right hand value to the left hand object

```ruby
# Hash literal notation
hash_literal = {
 "this" => "this",
 "is" => "is",
 "a" => "a",
 "hash" => "hash",
}

# Hash new
my_hash = Hash.new
my_hash["this"] = "this"
my_hash["is"] = "is"
```

## Syntax

```ruby
# This is a comment
number = 100
flag = true
str = "Ruby rocks"
str = "String redefined"

# Math
puts 30 + 20 - 2 * 4
puts 21 * 8 / 4
# I got the powerrrrr
puts 2 ** 6 - 22
# modulo math \m/
puts 142 % 50

# reversii
arr = ["a", "b", "c"]
print arr, arr.reverse.reverse
arr.each do |item|
  puts "Arr contains #{item}"
end

=begin
This
is
a
multiline
comment
=end

str = "string"
print "Lets interpolate this #{str}"

mutable = "Let's mutate this string"
mutable.capitalize!

is_expression = true
is_not_expression = true
if is_expression && !is_not_expression
  puts "Is an expression"
elsif !is_expression && is_not_expression
 puts "Is not an expression"
else
  puts "It both is and is not 🤷‍♂️"
end

is_expression = true
unless is_expression
  puts "Is not an expression"
else
  puts "Is an expression"
end

is_cold = false
while is_cold
  puts "Gettin' hot"
  is_cold = !is_cold
end

is_cold = false
unless is_cold
  puts "Gettin' hot"
  is_cold = !is_cold
end

# for loop with exclusive range
for v in 1...5
  puts v
end

# print even numbers
# use next to skip the odd numbers
def evens(n)
  for i in 1..n
    next if i % 2 != 0
    print i
  end
end


my_2d_array = [
	['x','-',-''],
	['x','o',-''],
	['x','o',-''],  
]

sweet_hash = {
	"a" => "is a",
	"b" => "bbbb",
	"c" => "c me",
}

sweet_hash.each{ |k, v| puts "#{k}: #{v}" }
hash_with_default = Hash.new("this is the default / empty value")

bad_hash = {
 "b" => 2,
 "d" => 4,
 "a" => 1,
 "c" => 3
}

bad_hash.sort_by { |k,v| k }          # [["a", 1], ["b", 2], ... ]
bad_hash.sort_by { |k,v| k }.reverse  # [["d", 4], ["c", 3], ... ]

def is_prime(n)
  false unless n.is_a? Integer
    is_prime = true
    for i in 2..n 
      if i % 2 == 0
        is_prime = false 
      end
    end
	end
  is_prime
end

def greet(greeting, *leute)
  puts "#{greeting} "
  leute.each do |human|
    puts "#{human}"
  end
end

# combined comparison operator
"a" <=> "b" # returns -1
"b" <=> "a" # returns 1
"b" <=> "b" # returns 0

# custom sorting block
nums = [0, 9, 3, 5, 2, 6, 4, 1, 7, 8]
nums.sort!{ |a, b| a <=> b } # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
nums.sort!{ |a, b| b <=> a } # [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]

def alphabetize(arr, rev=false)
	rev ? arr.sort!.reverse! : arr.sort!
end

numbers = [4,5,1,3,2]

puts alphabetize numbers      # [1,2,3,4,5]
puts alphabetize numbers,true # [5,4,3,2,1]

# Only 1 copy of a symbol can exist at a time
puts "string".object_id
puts "string".object_id

puts :symbol.object_id
puts :symbol.object_id

# Hash symbols can be defined in 2 ways
# Old way
movies = {
 :top_gun => "****",
 :vertigo => "*****"
}

# New way
movies = {
 top_gun: "****",
 vertigo: "*****"
}

case something
  when "value"
   block
  when "other value"
   block
  else
   block
end

# Ruby fu
<expression> if <condition>
<expression> unless <condition>
<condition> ? <true expression> : <false expression>
case <expression> when <value> then <expression> else <expression> end

my_array = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
my_array.each { |x| puts x if x.even? }

## print values from 10 - 20
10.upto(20) { |num| print num }
"a".upto("j") { |char| print char }

## check if an object can respond to a method
[1,2,3].respond_to?(:push) # returns true since you can push to an array
[1,2,3].respond_to?(:to_sym) # false, cant convert an array to a symbol

[1,2,3] << 4 # [1,2,3,4]
"Hello" << " " << "World" # "Hello World"
"I am " << age.to_s << " years old" # need to use .to_s on non-string values
```

## stdlib
### Methods
- `capitalize` capitalize the first letter of a string
- `chomp(str)` remove a trailing instance of _str_, if no argument is given it removes a single traliling new line _\n_
- `chop` removes the last char in a string or leaves an empty string unmodified
- `delete(!)` remove a key from a hash
- `each` iterate over key value pairs, takes a block
  - `each_key` iterate over keys only
  - `each_value` iterate over values only
- `gets` retrieves user input, it will automatically add a new line at the end
- `gsub` global substitution method for replacing using regex
- `include?` check for an occurence of the argument within the caller
- `is_a?` checks the type of the argument
- `length` output the length of the string
- `object_id` returns the internal id of an object, used to keep track of objects
- `print` outputs the arguments to the stdout, it can take a variable number of arguments
- `puts` outputs the arguments to the stdout and adds a blank line, takes a single argument
- `respond_to?` check if an object can respond to a method
- `reverse` reverse contents of some data
- `select` takes block returning items from the hash that meet the criteria, used for filter
- `sort` used to sort collections
  - blocks passed into sort need to return 1, 0 or -1
  - -1 = first parameter is before the second
  - 0 = parameters are equal
  - 1 = first parameter after the second
- `split` converts a string into an array based on a delimiter
- `times` takes a block and will execute it n times
- `to_<>`: convert between data types s => string, sym => symbol
  - intern => convert to symbol
- `upcase | downcase` change the casing of a string
- `upto | downto` used to print out a specific range of values

## Useful Links

- [Codeacademy - Ruby + Rails courses](https://www.codecademy.com/catalog/language/ruby)
