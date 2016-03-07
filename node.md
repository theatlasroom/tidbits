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

By convention callbacks should take 2 arguments err and data. `callback(err, data)`
- unless there is an error, the first arg should be null and the second will contain your data

### Events

### Streams
An API to exchange data., an abstraction to make it easy to move data from one place to another.
Readable and Writable are the 2 main types of streams.
The console standard output (process.stdout) is a stream

* use the .on(data) event to handle new data coming into the stream
* duplex streams can be both read and written to
* transform streams are duplex streams that transform the data (via a function) before it is read

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
### Web / Networks
#### [http]()
In order to support the full spectrum of possible HTTP applications, Node.js's HTTP API is very low-level. It deals with stream handling and message parsing only. It parses a message into headers and body but it does not parse the actual headers or the body.

- http.request: used to create a http request
- http.get(opts, [callback]): used to create GET request, same as request but sets the method to get and calls req.end() automatically. The callback receives 'response' which is a node stream object that emits various events, 3 of the events are: data, error and end. Calling setEncoding on the response with "utf8" will return a string instead of a buffer


#### [net]()
All basic networking functions for the node core

- net.createServer([callback(socket)]): takes a callback which is called everytime the server receives a connection, the callback takes a socket as its argument.
  * It will also return an instance of your server `server = net.createServer(callback)`
  * call server.listen(port) to start listening
- net.Socket: abstraction of a TCP / local socket
  * use socket.write to write data
  * socket.end() to close the socket, the end method also takes  a data object which will be written before sending the FIN (close socket) packet

### I/O
#### [fs]() - Filesystem module
  - All synchronous operations end with `Sync`
  - fs.readFileSync - returns a buffer object with the full contents of the file. Passing 'utf8' as the second argument will return a string
  - fs.readFile - async form readFileSync
  - readdir - takes a pathname and a callback(err, files), returns an array of the filenames in the dir
  - fs.createReadStream
  - fs.createWriteStream

#### [bl]()
Buffer list - allows you to have a stream piped into it and it will collect the data. Once the stream finishes a callback is fired with the collected data.
`response.pipe(bl(function (err, data) { /* ... */ }))`

#### [concat-stream]()
Similar to BL
`response.pipe(concatStream(function (data) { /* ... */ }))`

#### [path](https://nodejs.org/dist/latest-v5.x/docs/api/path.html)
  - path.basename(path, ext): returns the full base name, if you add the ext argument, it strips the extension from the value returned
  - path.delimiter: returns the platforms path delimiter
  - path.dirname: returns just the directory part of a path
  - path.extname: returns the extension of the path based on the last `.`
  - path.format: takes an object `{ root, dir, base, ext, name }` and returns a formatted path
  - path.isAbsolute: check if the path is an absolute value path
  - path.join([Array]): join all arguments (strings) together into a path
  - path.normalize: cleans up a dirty path (double slashes etc)
  - path.parse: returns an object `{ root, dir, base, ext, name }` from the path string
  - path.sep: path seperator

### Formatting
#### Dates

### Admin
* [pm2]() - Process monitoring

## NPM Packages
- strftime: unix style date formatting
- through2-map: allows you to create a transform stream using only a single function that takes a chunk of data and returns a chunk of data. It's designed to work much like Array#map() but for streams
