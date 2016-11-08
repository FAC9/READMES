### fs (File System) module

The file system module gives you control of the input and output (I/O) of files into your project. An example of this is giving your JavaScript file the ability to read the content of a different file.

When you install Node the fs module comes as default. To use this module you need to simply import it into your project like this:<br><br>
`var fs = require("fs")`

Interestingly all of the file system functions offer both synchronous `readFile` (blocking) and asynchronous `readFileSync` (non-blocking) versions.

Synchronous:

```
var contents = fs.readFileSync('DATA', 'utf8');
console.log(contents);
```

In this synchronous function the `console.log` will run when the DATA file has been read, no further code will run until this task is complete.

Asynchronous:

```
fs.readFile('DATA', 'utf8', function(err, contents) {
    console.log(contents);
});
```

In this asynchronous function the `console.log` will be added to the call stack when the DATA file has been read, but the JavaScript engine will keep processing the rest of the document until this happens.

Another key method of fs is `fs.writeFile`

`fs.writeFile(file, data[, options], callback)`- To write/create content in a file.

```
fs.writeFile('helloworld.txt', 'Hello World!', function (err) {
  if (err) return console.log(err);
  console.log('Hello World > helloworld.txt');
});
```

[contents of helloworld.txt]:
Hello World!

##### Other key fs module methods:<br>
- `fs.appendFile()` - method to append the content to an existing file.
- `fs.open(path, flags[, mode], callback)` - open a file for reading or writing.
- `fs.unlink(path, callback)` - delete an existing file.

### http module

like all node modules, the http module increases javascript functionality that it didn't need when it was created for the front-end. The http module contains the required functions and properties to implement http servers and http clients (a HTTP client uses HTTP to connect to a web server over the Internet to transfer documents or other data).

Like fs, http is a core module which is included when you install Node. To use the http module you import it in the same way as all core modules: <br>

`var http = require("http")`

9/10 times (I made this stat up), we will be using the http module to create web servers. Here is the code to do this:

```
//Lets import the HTTP module
var http = require('http');

//Lets define a port we want to listen to
const PORT=8000;

//We need a function which handles requests and send response
function handleRequest(request, response){
    response.end('It Works!! Path Hit: ' + request.url);
}

//Create a server
var server = http.createServer(handleRequest);

//Lets start our server
server.listen(PORT, function(){
    //Callback triggered when server is successfully listening. Hurray!
    console.log("Server listening on: http://localhost:%s", PORT);
});
```

##### key http module methods:
- `http.createServer()` - returns a new Server object.
- `server.listen()` may be called multiple times, each time re-opening the server.
- `server.on()` - allows you to bind callbacks to events.
- `server.close()` - stops the server from accepting new connections.
