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

LWOP
-


# django
- activate a virtualenv use: `source bin/activate`
  - **mkvirtualenv** - create a new virtual env
  - **workon** - switch to an existing virtual env
- you can create projects or apps
- apps are modules that can be reused and perform a task
- projects are collections of apps and configs for a website
- settings.py

## Models
- Built in ORM:
  - obj = Model(fields) -> create a new objects
  - obj.save() -> save changes to the object
  - obj.create() -> create and save changes in one step
  - Model.objects.all() -> return all from a model collection
  - Model.objects.filter(field=value) -> return objs that match the query set
  - Model.objects.exclude(field=value) -> opposite to filter
  - Model.objects.get()
- Field lookups
  - used to make sql where queries
  - field__lookuptype=value
  - Entry.objects.filter(pub_date__lte='2006-01-01') -> SELECT * FROM blog_entry WHERE pub_date <= '2006-01-01';
  - exact -> exact match
  - iexact -> case insensitive match
  - contains -> where Like ...
  - startswith, endswith, istartswith, iendswith
  - works on joins
    - Blog.objects.filter(entry__headline__contains='Lennon') -> select * from Blog join entry on headline contains 'Lennon'

## Views
- generic views are used to handle reused logic
- generic.ViewType (ListView, DetailView etc) -> abstract definitions of a type of view for an object. ie list of objects, details view etc
  - needs to know what model to act on (model attribute)
  - DetailView generic expects primary key value captured from the url to be 'pk'
  - ListView defaults to used a view in the form `<app name>/<model name>_list.html`
  - DetailView defaults to used a view in the form `<app name>/<model name>_detail.html`
  - context_object_name attribute used to overwrite default name sent to the view as a context
  - template_name overwrites the default template with one we specify
- decorators can be used to limit access based on request method
  - uses django.views.decorators.http.require_http_methods
  - before the view method, write `@require_http_methods(["GET", "POST"])`


## Tests
- Client - used to simulate a user interacting with the code from the level of a view

## Managers
- Interface for database query operations
- At least 1 exists for every model
- By default a manager with the name **objects** is added to every model call
  * to rename, define a class attribute on that model ie people = models.Manager()
- Base QuerySet returns all objects in the system
- You can attach as many managers as you want to a model
  * good way to define custom filters
### Adding methods to a manager
- [more info](https://docs.djangoproject.com/en/1.8/topics/db/managers/#adding-extra-manager-methods)
- 'Table level functions' can be added as extra Manager methods
- Model methods can be used to add 'row level functions' ie functions on a specific row


## settings.py
- all apps need to be added to the INSTALLED_APPS setting

## URLs
### General
- the urlconf doenst check for request methods like POST/GET et
  - all request methods would be routed to the same function for the same url
- Captured arguments are always strings
- named regular expresssions have the format (?P<name>pattern)
  - name is the name of the group
  - pattern is what is matched
  - Regex: url(r'^<article></article>es/(?P<year>[0-9]{4})/$', views.article_detail) -> views.article_detail(request, year='2003').
- Generating urls for entites can be done in 3 ways
  - In templates: Using the url template tag.
  - In Python code: Using the django.core.urlresolvers.reverse() function.
  - In higher level code related to handling of URLs of Django model instances: The get_absolute_url() method.
  - named urls must be used to be able to do this

### urls.py
- url takes 4 arguments
  - [regex](https://docs.python.org/3/library/re.html#raw-string-notation): pattern used to match the url against, does not include get / post params or the domain name
  - view: django calls the specified view function with a HttpRequest obj as the first argument and any capture values as other args.
  - kwargs: arbitary keywords passed to the view as a dictionary
  - name: name for the url, used within your application to refer to the url

## django-rest-framework
- uses serializers to connect models to the the outside world
- serializers.ModelSerializer adds shortcuts for extending a model
- HyperlinkedModelSerializer
  - does not include pk field
  - includes a url field, using HyperlinkedIdentityField
  - HyperlinkedRelatedField instead of PrimaryKeyRelatedField

### APIS / Request / Response / status
- Request
  - an object that extends HttpRequests and provides more flexibility
  - request.data: handles arbitrary data, works for POST, PUT, PATCH
- Response
  - a type of TemplateResponse that takes unrendered content and uses content negotiation to determine the correct content type to return to the client
  - return Response(data) - renders to clients requested content type
- Status: provides friendlier status codes such as HTTP_400_BAD_REQUEST
- 2 options for writing API views
  - The @api_view decorator for working with function based views.
  - The APIView class for working with class based views.
  - The wrappers also provide behaviour such as returning 405 Method Not Allowed responses when appropriate, and handling any ParseError exception that occurs when accessing request.data with malformed input.

## manage.py
- runserver: runs the python server on the port specified (or default)
- check: check for any issues with your project
- makemigration (appname): generates migrations for the app, based on the models defined + any latests changes to the models
- migrate: run db migrations
- startapp (appname): creates a new app
- sqlmigrate (app) (migration number): lets you preview the sql that will be generated from your migration
- shell: play around with the free api + imports the django settings and environment vars
- test 'suitename' - runs tests
- createsuperuser -  create a super user account


## Notes
* IndentationError: expected an indented block - you should indent your code with 4 spaces

## useful links
* [Setting up virtualenvs](http://hackercodex.com/guide/python-development-environment-on-mac-osx/)
