# NodeJS
## Installation
* Don't install node directly, set it up using [nvm](https://github.com/creationix/nvm)
* [Run npm commands without sudo](https://docs.npmjs.com/getting-started/fixing-npm-permissions)

## General
Importing / Requiring packages
Use the require command to load globally available node modules
`var fs = require('fs')`

### Command line arguments:
You can access command-line arguments via the global process object. The  
process object has an argv property which is an array containing the  
complete command-line. i.e. `process.argv`

### Type Coercion
Number() - convert to Number
String() - to string

### Buffers
Buffer objects are Node's way of efficiently representing arbitrary arrays  
of data, whether it be ascii, binary or some other format. Buffer objects  
can be converted to strings by simply calling the toString() method on  
them. e.g. `var str = buf.toString()`.  

### Strings

### Numbers

## Packages
### I/O
* [fs]() - Filesystem module
  - All synchronous operations end with `Sync`
  - fs.readFileSync - returns a buffer object with the full contents of the file. Passing 'utf8' as the second argument will return a string

### Admin
* [pm2]() - Process monitoring
