### Module 18
#### NodeJS Setup
The only thing you need to run nodejs is to install it.
There are several ways to do it, we recommend checking the offcial website and downloading the LTS(Long Term Support) version.
#### Introduccion
Node.js is a server-side platform built on Google Chrome's JavaScript Engine (V8 Engine). Node.js was developed by Ryan Dahl in 2009.
Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient, perfect for data-intensive real-time applications that run across distributed devices.
##### Features of Node.js

Following are some of the important features that make Node.js the first choice of software architects.

-   **Asynchronous and Event Driven** − All APIs of Node.js library are asynchronous, that is, non-blocking. It essentially means a Node.js based server never waits for an API to return data. The server moves to the next API after calling it and a notification mechanism of Events of Node.js helps the server to get a response from the previous API call.
    
-   **Very Fast** − Being built on Google Chrome's V8 JavaScript Engine, Node.js library is very fast in code execution.
    
-   **Single Threaded but Highly Scalable** − Node.js uses a single threaded model with event looping. Event mechanism helps the server to respond in a non-blocking way and makes the server highly scalable as opposed to traditional servers which create limited threads to handle requests. Node.js uses a single threaded program and the same program can provide service to a much larger number of requests than traditional servers like Apache HTTP Server.
    
-   **No Buffering** − Node.js applications never buffer any data. These applications simply output the data in chunks.
##### Where to Use Node.js?

Following are the areas where Node.js is proving itself as a perfect technology partner.

-   I/O bound Applications
-   Data Streaming Applications
-   Data Intensive Real-time Applications (DIRT)
-   JSON APIs based Applications
-   Single Page Applications

##### Where Not to Use Node.js?

It is not advisable to use Node.js for CPU intensive applications.
#### Global Object
The global object in node is the `globalThis` which is equal to the `global` object, this object has the built-in methods like `setTimeout`, `setInterval`, and another methods.
Unlike the browser `this` is not equal to the `global` which is the global object, instead `this`  makes reference to the `module.exports` object, there are objects or properties that may be confused with global objects, but this objects or properties have module scope, such as:
- `__dirname`
- `__filename`
- `exports`
- `require`
- `module`
Global objects and classes are:
- `AbortController` class
- `AbortSignal` class
- `Buffer` class
- `setImmediate`
- `clearImmediate`
- `setInterval`
- `clearInterval`
- `setTimeout`
- `clearTimeout`
- `console`
- `Event`
- `EventTarget`
- `MessageChannel`
- `MessageEvent`
- `MessagePort`
- `process`
- `queueMicrotask`
- `TextDecoder`
- `TextEncoder`
- `URL`
- `URLSearchParams`
- `WebAssembly`
#### HTTP Module
To make HTTP requests in Node.js, there is a built-in module **HTTP** in Node.js to transfer data over the HTTP. To use the HTTP server in node, we need to require the HTTP module. The HTTP module creates an HTTP server that listens to server ports and gives a response back to the client.
**Syntax:**

```js
var http = require('http');
```
##### Create an HTTP Server
We can create a HTTP server with the help of `**http.createServer()**` method.
```js
const http = require('http');

const Server = http.createServer((req, res) => {
  res.writeHead(200, {'Content-Type': 'text/plain'});
  res.write('Aronis wishes u happy holidays! \n');
  res.write(`URL from request ${req.url} \n`);
  res.write(`Address from request ${req.connection.remoteAddress} \n`);
  res.write(`Headers from request ${JSON.stringify(req.headers)} \n`);
  res.end();
});

Server.listen(3000);
.listen(3000); // Server listening on port 3000
```
Output:
```
node server.js
Server started on port 3000
```
`Server.listen()` Binds the server to listen to a specific port, this port binding is subject to permission restrictions, Unix TCP/IP ports bellow 1024 are privileged ports, so if you try to listen to port 80 (HTTP default port) your user running the node app might need special permissions, such as `sudo`.
`Server.close()` stops the server from listening to more requests, unbinds the server from the port.
##### Inside the callback to handle HTTP request
`req`: shorthand for request, is an object from the class  IncomingMessage that includes all the request information. Some interesting properties are:
-   `req.connection` contains all the connection information pertinent to the request such as .remoteAddress, that contains the network address that originated or forwarded the request.
-  ` req.headers` includes the headers attached to the request. If you visited the application at localhost:300 with your browser, one of the headers you would get is "user-agent" which includes information about the browser.
*note*: each request object is, indeed, a stream.
`res`: shorthand for "response", is an object from the class ServerResponse, which contains a collection of methods to send back an HTTP response. Some of the methods are:
-   `.writeHead()` should be called first when initiating a response, allows us to set up the HTTP response code and headers we are sending back.
-   .`write(chunk[, encoding][, callback])` allows us to send a chunk of data as part of our response. In this case, we declared in the header the content-type as 'text/plain', so each time we write() the data we pass gets attached as a string of text.
    `chunk` could be either a buffer or a string, in the case, it is a string the second parameter which is optional, allows us to set the encoding of the data being sent, the default value is `'utf8'`.
    The third parameter is a callback function to be executed when the chunk of data has been sent.
    The first call to .write() will send the headers established in .writeHeader() or send the default ones.
    
-   `.end()` signalizes the response as complete, MUST be called once per response.
##### Handling POST request 
```js
const http = require('http');


const Server = http.createServer( (req, res) => {
  // If the request is a POST 
  // we try to parse the body
  if(req.method === 'POST'){
    let body = '';

    // We listen to the even data
	// In the request stream for the body
    req.on('data', chunk => {
      body += chunk.toString();
    });

	// We listen for the end of the stream
    req.on('end', () => {
      
      // We check the headers
	  // if we are getting a json object
      // We parse it from the string we gen
      if(
        req.headers["content-type"] === 'application/json'
      ) body = JSON.parse(body);
      
      console.log(body);
	  // We must always end the response
      res.end('ok');
    });
  }
});

Server.listen(3000);
```
##### Make HTTP Request
To make requests via the HTTP module ``**http.request()**`` method is used.
```js
var http = require('http');
  
var options = {
    host: 'www.geeksforgeeks.org',
    path: '/courses',
    method: 'GET'
};
  
// Making a get request to 
// 'www.geeksforgeeks.org'
http.request(options, (response) => {
  
    // Printing the statusCode
    console.log(`STATUS: ${response.statusCode}`);
}).end();//body goes gere inside the end method
```

#### File System
The `fs` module provides a lot of very useful functionality to access and interact with the file system.
-   `fs.access()`: check if the file exists and Node.js can access it with its permissions
-   `fs.appendFile()`: append data to a file. If the file does not exist, it's created
-   `fs.chmod()`: change the permissions of a file specified by the filename passed. Related: `fs.lchmod()`, `fs.fchmod()`
-   `fs.chown()`: change the owner and group of a file specified by the filename passed. Related: `fs.fchown()`, `fs.lchown()`
-   `fs.close()`: close a file descriptor
-   `fs.copyFile()`: copies a file
-   `fs.createReadStream()`: create a readable file stream
-   `fs.createWriteStream()`: create a writable file stream
-   `fs.link()`: create a new hard link to a file
-   `fs.mkdir()`: create a new folder
-   `fs.mkdtemp()`: create a temporary directory
-   `fs.open()`: set the file mode
-   `fs.readdir()`: read the contents of a directory
-   `fs.readFile()`: read the content of a file. Related: `fs.read()`
-   `fs.readlink()`: read the value of a symbolic link
-   `fs.realpath()`: resolve relative file path pointers (`.`, `..`) to the full path
-   `fs.rename()`: rename a file or folder
-   `fs.rmdir()`: remove a folder
-   `fs.stat()`: returns the status of the file identified by the filename passed. Related: `fs.fstat()`, `fs.lstat()`
-   `fs.symlink()`: create a new symbolic link to a file
-   `fs.truncate()`: truncate to the specified length the file identified by the filename passed. Related: `fs.ftruncate()`
-   `fs.unlink()`: remove a file or a symbolic link
-   `fs.unwatchFile()`: stop watching for changes on a file
-   `fs.utimes()`: change the timestamp of the file identified by the filename passed. Related: `fs.futimes()`
-   `fs.watchFile()`: start watching for changes on a file. Related: `fs.watch()`
-   `fs.writeFile()`: write data to a file. Related: `fs.write()`
One peculiar thing about the fs module is that all the methods are asynchronous by default, but they can also work synchronously by appending Sync.
For example:
-   `fs.rename()`
-   `fs.renameSync()`
-   `fs.write()`
-   `fs.writeSync()`
#### Events
The `events` module provides us the EventEmitter class, which is key to working with events in Node.js.
```js
const EventEmitter = require('events')
const door = new EventEmitter()
```
The event listener has these in-built events:
- `newListener` when a listener is added
- `removeListener` when a listener is removed
- `emitter.addListener()`
	Alias for `emitter.on()`.
- `emitter.emit()`
Emits an event. It synchronously calls every event listener in the order they were registered.
```js
door.emit("slam") // emitting the event "slam"
```
- `emitter.on()`
Adds a callback function that's called when an event is emitted.
Usage:
```js
door.on('open', () => {
  console.log('Door was opened')
})
```
-  `emitter.removeListener()`
Remove a specific listener. You can do this by saving the callback function to a variable, when added, so you can reference it later:
```js
const doSomething = () => {}
door.on('open', doSomething)
door.removeListener('open', doSomething)
```
#### NodeJS vs Browser
You don't have `document`, `window` and all the other objects that are provided by the browser.

And in the browser, we don't have all the nice APIs that Node.js provides through its modules, like the filesystem access functionality.

Another big difference is that in Node.js you control the environment. Not like in browser that your target are all the browser that the user can use.  This means that you can write all the modern ES6-7-8-9 JavaScript that your Node.js version supports.

Another difference is that Node.js uses the CommonJS module system, while in the browser we are starting to see the ES Modules standard being implemented.

The global object is not the same also, the this keyword only apply in the module context, not like in browsers.
#### Databases Overview
There are many databases technologies, nodejs has packages to work with most of those options, and most of those options fall into two categories `SQL` or `NoSQL`
- `SQL`: 
	- Structured Query Language
	- Up-front design
	- Sometimes perfomrance and query benefits
	- Sometimes performance hits from overhead
- `NoSQL`
	- No structure, just collections of any data.
	- Less or no up-front design
	- Sometimes performance gains
You can access to databases in nodejs and create, read, update, delete with your application, even if they are locally or hosted databases
	