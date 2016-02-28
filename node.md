# NodeJS
Evented programming lib in JS
* when a operation is dispatched, node will wait for it to return an event indicating it is completed
* while waiting, node can do other things
* Node will loop over all the operations that have been dispatched and check if any are now finished
* Once an operation is finished, node processes its callback(s) by invoking each of them

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

### Callbacks
Callbacks are functions that are executed asynchronously.
The order of execution of a function depends on the speed of the previous functions.
Determining if a function is async or not can depend on the context it is in.
Operations that have I/O to either disks, or networks, databases etc will be typically async, operations that read from memory or just use the cpu will usually be sync.
Callbacks are just functions that get executed at a later time.

`var fs = require('fs');

// define our callback
function cb(){
  console.log("Callback executed");
}

// define our function
function readNumber(callback){
  fs.readFile('some-file.txt', function(err, content){
    var num = parseInt(content);
    console.log("Read number " + num);
    callback(); // the callback is the last operation in the closure that is executed when the readfile operation completes
  })
}

// invoke the readNumbr function and pass the callback as a parameter to the function
readNumber(cb);
`

### Events

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
