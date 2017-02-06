# Hapi
Application framework for nodejs

## API
* Server: the main application container, manages connections
  - new Server([options]) creates a new server, with options specified such as:
    * app - application config
    * cache - server side application caching, by default hapi uses catbox
    * connections - sets the default connections
      - app - used to store application configurations
      - compression - defaults to true
      - load
      - plugins - plugin specific configuration, accessed via connection.settings.plugins
      - router - controls how incoming request uris are handled
      - routes - sets the default config for routes
      - state - default config for state
    * plugins - plugin specific configuration, accessed via server.settings.plugins
  - the server can contain more than 1 connection (listening on multiple ports)
  - server.settings.app: stores static config
  - server.app: stores run time application state
  - .app - place to store server specific runtime data, initialized with an empty object
  - .connections - an array of the connections for the server
  - .info - information about a connection
    * id - unique connection identifier
    * created - connection created timestamp
    * started - connection start timestamp
    * port - either the port value before the server was started, or the actual port assigned when no port is configured
    * host - the hostname the connection was configured to
    * address - active IP addresses the connection was bound to
    * protocol - the protocol used http/s, socket
    * uri - string representing the connection
    * this property is available here when there is only 1 connection, otherwise available from server.connections
  - .mime - access to the server MIME database used for setting content-type information
  - .plugins - object containing the values exposed by each plugin registered where each key is a plugin name and values are exposed by the plugin using the server.expose() function
  - .root - root serevr object, with all the connections and access to methods start(), stop(), connection
  - .settings - the configuration object after defaults are applied
  - .auth.api - auth strategies
  - .auth.default - default auth strategy
  - .auth.scheme - registers an authentication scheme
  - .auth.strategy - registers an auth strategy
  - .auth.test - tests a request against an auth strategy
  - .initialize - initializes a server but does not start listening on the connection ports, returns a promise or executes a callback
  - .inject - simulates an incoming http request without making a socket connection, useful for testing or internal routing logic
  - .log - logs server events
  - .lookup - looks up a route configuration, takes a route identifier
  - .match - looks up a route configuration, takes a http method, requested path and optional host
  - .method - registers a server method function
  - .on - subscribe an event listener
  - .path - sets the path prefix used to locate static resources
  - .route - adds a connection route
  - .state - use client cookies to persist a state across multiple requests
  - .table - returns a copy of the routing table



## Plugins
- catbox: provides cache storage options such as memcached, redis etc
- joi: object schema validation, used to validate request and response objects based on schemas
- hapi-swagger: interface to Swagger
- hapi-raven: Sentry logging, using the [raven package](https://www.npmjs.com/package/raven) for node
- hapi-auth-cookie

## Links
* [Official docs](https://hapijs.com/)
