# Ruby

## General

- High level, _interpreted_, _oo_
- Developed by Yukihiro Matsumoto (Matz)
- Everything is an object
- local variables should lowercase with `snake_casing`
- `method!` methods mutate their caller

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
```

## stdlib

- `capitalize` capitalize the first letter of a string
- `chomp(str)` remove a trailing instance of _str_, if no argument is given it removes a single traliling new line _\n_
- `chop` removes the last char in a string or leaves an empty string unmodified
- `gets` retrieves user input, it will automatically add a new line at the end
- `.length` output the length of the string
- `print` outputs the arguments to the stdout, it can take a variable number of arguments
- `puts` outputs the arguments to the stdout and adds a blank line, takes a single argument
- `.reverse` reverse contents of some data
- `.upcase | .downcase` change the casing of a string

## Useful Links

- [Codeacademy - Ruby + Rails courses](https://www.codecademy.com/catalog/language/ruby)
