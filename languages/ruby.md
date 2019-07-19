# Ruby

## General

- High level, _interpreted_, _oo_
- Developed by Yukihiro Matsumoto (Matz)
- Everything is an object
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
```

## stdlib

- `capitalize` capitalize the first letter of a string
- `chomp(str)` remove a trailing instance of _str_, if no argument is given it removes a single traliling new line _\n_
- `chop` removes the last char in a string or leaves an empty string unmodified
- `gets` retrieves user input, it will automatically add a new line at the end
- `gsub` global substitution method for replacing using regex
- `include?` check for an occurence of the argument within the caller
- `length` output the length of the string
- `print` outputs the arguments to the stdout, it can take a variable number of arguments
- `puts` outputs the arguments to the stdout and adds a blank line, takes a single argument
- `.reverse` reverse contents of some data
- `.split` converts a string into an array based on a delimiter
- `.times` takes a block and will execute it n times
- `.upcase | .downcase` change the casing of a string

## Useful Links

- [Codeacademy - Ruby + Rails courses](https://www.codecademy.com/catalog/language/ruby)
