# Elixir

## Case

- compares patterns to different _values_ and will return the first true match
- a `CaseClauseError` will be raised if no patterns match

```
case {1,2,3} do
  {4,5,6} -> "No match"
  {1,x,3} -> "Matches and binds x to 2"
  _ -> "Match anything"
end
```

- existing values can be pattern matched with the `^` operator

```
x = 1
case 10 do
  ^x -> "Won't match"
  _ -> "Will match"
end
```

- guards can also be applied to add extra conditions

```
iex> case {1, 2, 3} do
  {1, x, 3} when x > 0 -> "Will match"
  _ -> "Would match, if guard condition were not satisfied"
end
```

- anonymous functions can be matched if they have the same number of parameters

```
f = fn
  x, y when x > 0 -> x + y
  x, y -> x * y
end
```

## Cond

- Similar to case
- Used for pattern matching against different _conditions_, returning the first that returns true
- A `CondClauseError` will be raised if no condition returns true, adding a default true condition will avoid this
- Any value except `nil` and `false` will be truthy

```
cond do
  2 + 2 == 5 ->
    "This is never true"
  2 * 2 == 3 ->
    "Nor this"
  true ->
    "This is always true (equivalent to else)"
end
"This is always true (equivalent to else)"
```

## General notes

- String concatenation uses `<>`
- Modules start with a capital, names of modules are valid atoms even if they have not been declared yet
- Atoms are used to reference modules from Erlang libraries
- `or`, `and`, `not` expect a boolean on the left side
- `||`, `&&`, `!` can operate on any type
- integer division and modulo use the functions `div` and `rem`
- any two types can be compared, the rules for ordering sorted types are

```
number < atom < reference < function < port < pid < tuple < map < list < bitstring
```

- lists are collections containing any type, they can include non-unique values
- prepending is faster than appending as lists are implemented as linked lists
- `++` can be used for list concatenation, `--` for subtraction (subtract right list from left),
  - if items are duplicated only the first instance is removed
  - comparison is done using the strict comparison operator `===`
- `hd` returns the head, `tl` returns the tail
- `|` splits a list into head and tail, ie _[head | tail] = [1 2 3]_ -> returns head=1 and tail =[2,3]
- tuples can hold any type, are stored contiguously in memory, and declared with curly braces `{"tuple", "of", "strings"}`
  - fast to access length
  - slow to modify and
  - useful for return types from functions as they can be pattern matched
- all collections except tuples are enumerable
  - `Enum` module provides a range of useful functions for enumerables
    - Enum.`min|max|map|filter|reduce|each|sort|uniq_by`
  - `Enum.all?(list, fn)` evaluate the function against each elemnt of the list and return true if they all evaluate to true
  - `Enum.any?(list, fn)` evaluate the function against each elemnt of the list and return true if any results in true
  - `Enum.chunk_every(list, chunk_size)` split the list into `chunk_size` groups
  - `Enum.chunk_by(list, fn)` split into groups based on the function
  - `Enum.map_every(list, nth_item, fn)` apply the map function to each `nth` item of the list
- `if` and `unless` are supported
- `_` matches against any item
- `case ... do end` allowas matching against multiple patterns
  ```
  case {:ok, "Hellow World"} do
    {:ok, result} -> result
    {: error, result} -> error
    -> "Catch all"
  end
    ->
  ```
- `cond do end` matches conditions instead of values

```
cond do
  2 + 2 == 5 -> failed_test
  1 + 1 == 5 -> passed_test
  true -> default_result
end
```

- `with` can be used to pattern match in place of `case`

```
user = %{first:, "Sean", last: "Callan"}
with {:ok, first } <- Map.fetch(user, :first),
     {:ok, last } <- Map.fetch(user, :last),
     do: last <> ", " <> first
```

- anonymous functions can be defined in multiple ways

```
sum = fn (a,b) -> a + b end
also_sum = &(&1 + &2)
sum.(2,3) // outputs 5
also_sum.(2,3) // outputs 5
```

- functions can be defned using pattern matching, allowing for variable arguments to be passed

```
handle_result = fn
  {:ok, result} -> IO.puts "Handling result..."
  {:ok, _} -> IO.puts "Wont match as the previous result will"
  {:error} -> IO.puts "An error has occured"
end
```
