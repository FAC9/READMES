# Node fundamentals
Create a readme on the methods and properties you find most useful for the group to know.

##### fs (File System) module

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

### Investigate the core modules: url, path, querystring, and their methods. (Marko)
Create a readme on this topic

### Investigate the request and response objects, what are some of their useful properties? (Lucy)
Create a readme on this topic

### Look into module.exports. How does it work (Nori)

```module.exports``` is the object that's actually returned as the result of a ```require``` call.

The ```exports``` variable is a shorthand alias for ```module.exports``` and it's initially set to that same object. 

![module_export](./images/modules_explained.jpg)

#### What is a module?
A module encapsulates related code into a single unit of code. In practice creating a module often means moving all related code into a file.

```
// simple_math.js
function add (a,b) {
     return a+b;
};

function multiple(a,b){
     return a*b;
};

```
#### How to export a module
 
Our simple_math.js file becomes more useful if the functions can be utilized elsewhere. We can refactor in three steps.

-  Default values for ```exports``` and ```module.exports```.

```
  var exports = module.exports = {};
```

- We have to assign all the expressions to the export object that we want to be available in other files.
There is more than one way to do this:

```
exports.add = function(a,b){return a+b;};
exports.mutiple =function(a,b){return a*b;};
```

```
module.exports = {
     add : function(a,b){return a+b;};
     multiple: function(a,b){return a*b;};
};
```

Now ```exports``` and ```module.exports()``` all reference the same object.

#### Importing a module
 Let's import all our  math functions to main.js.

- Node.js uses the ```require``` keyword to import modules. How one can imagine the implementation of require.

```
var require = function(path){
     //code
     return module.exports;
};
```

-  Require simple_math in main.js

```
var simple_math = require('./simple_math');
simple_math.add(1,2);
simple_math.multiple(3,4);
```

#### module.exports vs export in Node.js

Just for explanation you can imagine that at the beginning of your file there is this code.
```
var module = new Module(...);
var exports = module.exports;
```

![module.exports vs exports](./images/exports_vs_moduleexports.png)


When you add 2 functions you can do this:
```
exports.add = function(a,b) {
    return(a+b);
}
exports.multiple = function(a,b) {
    return(a*b);
}
```
Now you are adding the add and the multiple function to the object on which ```module.export``` points. Now the returned object will be ```{add : [function],multiple :[function]}```. Note: in this case you get the same result if you use ```module.exports``` instead of ```exports```.
In this case ```module.exports``` is the container of the exported values.

It is possible that you only want to export a single function. It is possible, you can do something like this.

```
module.exports = function Message() {
    console.log("This is the sole function returned");
}
```
In this case ```module.exports``` returns a function, which van be immediately invoked.
```
var msg = require('./sample.js')();
```
NOTE! In this case you can't use the following assignment:
```
exports = function Message() {
    console.log("This is the sole function returned");
}
```

Because with this ```exports``` reference doesn't 'point' anymore to the object where ```module.exports``` points, so there is not a relationship between ```exports``` and ```module.exports``` anymore. In this case module.exports still points to the empty object {} which will be returned.

We  overrode ```exports```, ```exports``` refers to a new object, while ```module.exports``` refers to the original object. When we require the file, the object, to which ```module.export``` refers will be returned.

#### Resources

- [sitepoint tutorial](https://www.sitepoint.com/understanding-module-exports-exports-node-js/)
- [YouTube tutorial](https://www.youtube.com/watch?v=qLc29euevzc&index=14&list=PLrUFyg1unBb88J0r7gvJ1T01WN_pp83Lz)
- [bytearcher.com](http://bytearcher.com/articles/writing_modules/)
- [liangzan blog](http://blog.liangzan.net/blog/2012/06/04/how-to-use-exports-in-nodejs/)
