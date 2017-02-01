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

## Plugins
- catbox: provides cache storage options such as memcached, redis etc
- hapi-swagger
- hapi-raven: Sentry logging, using the [raven package](https://www.npmjs.com/package/raven) for node

## Links
* [Official docs](https://hapijs.com/)
