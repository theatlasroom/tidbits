# django
- activate a virtualenv use: `source bin/activate`
  - **mkvirtualenv** - create a new virtual env
    * `-p` to specify the python executable to use
    * `-a` specify a path to the env
  - **workon** - switch to an existing virtual env
- you can create projects or apps
- apps are modules that can be reused and perform a task
- projects are collections of apps and configs for a website
- settings.py

## Setup
`pip install Django==(version)` - check the django website for the latest version
`django-admin.py startproject <name> <dir>` to create a new django project

## Models
- Built in ORM:
  - obj = Model(fields) -> create a new objects
  - obj.save() -> save changes to the object
  - obj.create() -> create and save changes in one step
  - Model.objects.all() -> return all from a model collection
  - Model.objects.filter(field=value) -> return objs that match the query set
  - Model.objects.exclude(field=value) -> opposite to filter
  - Model.objects.get()
  - .values() allows you to specify the fields to be returned from the QuerySet
  - .values_list() returns values as a list obj
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

### QuerySets
- Model.objects.create(<params>): create a new instance of a model, optionally takes a list of parameters that map to attributes of the model
- .get_or_create(params): get or create the object if it doesnt exist
- Model.save(): save an object
- ...get(params): gets an object that matches the params

### Managers
- used to handle some of the logic behind the model
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

## Commands
- used to run commands to manager our application


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
- function views are simply functions that return a http response
- class views

## Django admin
- admin.py defines the models available able in the admin interface
- import the model you would like to use then register it using `admin.site.register(MODEL_NAME)`

## Tests
- Client - used to simulate a user interacting with the code from the level of a view

## settings.py
- all apps need to be added to the INSTALLED_APPS setting
- `ALLOWED_HOSTS` specifies the hosts to use to access the application
- 'TEMPLATES.DIRS' specifies the locations to check for template files
  * outer directories will be searched first before app dirs

## Shortcuts
- `get_object_or_404(class, filter)` - filters a class for a specific object and will return a 404 error if it doesnt exist

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
  - `django.core.urlresolvers` can be used to resolve urls

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

## django-hosts
- used to manage subdomains for your application

### APIS / Request / Response / status
- Request
  - an object that extends HttpRequests and provides more flexibility
  - request.data: handles arbitrary data, works for POST, PUT, PATCH
- Response
  - a type of TemplateResponse that takes unrendered content and uses content negotiation to determine the correct content type to return to the client
  - return Response(data) - renders to clients requested content type
- Status: provides friendlier status codes such as HTTP_400_BAD_REQUEST
- function based views handle all methods, the method use is available from the `request.method` paramater
- class based views require you to write methods for each request method that is supported
- 2 options for writing API views
  - The @api_view decorator for working with function based views.
  - The APIView class for working with class based views.
  - The wrappers also provide behaviour such as returning 405 Method Not Allowed responses when appropriate, and handling any ParseError exception that occurs when accessing request.data with malformed input.

## SPAs

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
