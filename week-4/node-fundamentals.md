# Node fundamentals
Create a readme on the methods and properties you find most useful for the group to know.

### Investigate the core modules: http, fs, and their methods. (Peter)

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

#### a) URL module

The URL module is used for URL resolution and parsing. It can be accessed using `require('url')`.

URL strings can be parsed into an object that contains a property for each of the URL string components. The following two methods are used for interconversion:
- `url.parse()` takes a URL string, parses it, and returns a URL object
- `url.format()` method takes a URL object and returns a formatted URL string

** Components of a parsed URL **  
_(using http://user:pass@host.com:8080/p/a/t/h?query=string#hash as an example URL)_

```html
┌─────────────────────────────────────────────────────────────────────────────┐
│                                    href                                     │
├──────────┬┬───────────┬─────────────────┬───────────────────────────┬───────┤
│ protocol ││   auth    │      host       │           path            │ hash  │
│          ││           ├──────────┬──────┼──────────┬────────────────┤       │
│          ││           │ hostname │ port │ pathname │     search     │       │
│          ││           │          │      │          ├─┬──────────────┤       │
│          ││           │          │      │          │ │    query     │       │
"  http:   // user:pass @ host.com : 8080   /p/a/t/h  ?  query=string   #hash "
│          ││           │          │      │          │ │              │       │
└──────────┴┴───────────┴──────────┴──────┴──────────┴─┴──────────────┴───────┘
```

| property name | description | example output |
|---|---|---|
| `urlObject.href` | the full URL string that was parsed (converted to lower-case) |  |
| `urlObject.protocol` | the protocol scheme | `'http:'` |
| `urlObject.auth` | username and password portion of the URL | `'user:pass'` |
| `urlObject.host` | full host portion of the URL, including the port | `'host.com:8080'` |
| `urlObject.hostname` | host name portion of the host component, without the port included |  `'host.com'` |
| `urlObject.port` | the numeric port portion of the host component | `'8080'` |
| `urlObject.pathname` | the entire path section of the URL | `'/p/a/t/h'` |
| `urlObject.search` | the entire "query string" portion of the URL, including the leading `'?'` character | `'?query=string'` |
| `urlObject.path` | a concatenation of the pathname and search components | `'/p/a/t/h?query=string'` |
| `urlObject.query` | the "params" portion of the query string, or an object returned by the querystring module's parse() method | `'query=string'` or `{'query': 'string'}` |
| `urlObject.hash` | the "fragment" portion of the URL | `'#hash'` |

#### b) Path module

The path module is used for working with file and directory paths. It can be accessed using `require('path')`.

Just like URLs, path strings can also be parsed into objects, and vice versa:
- `path.parse()` returns an object whose properties represent significant elements of the path
- `path.format()` returns a path string from an object

** Components of a parsed path **
_(using '/home/user/dir/file.txt' as an example path, on POSIX)_
```html
┌─────────────────────┬────────────┐
│          dir        │    base    │
├──────┬              ├──────┬─────┤
│ root │              │ name │ ext │
"  /    home/user/dir / file  .txt "
└──────┴──────────────┴──────┴─────┘
```

| method name | description | example output |
|---|---|---|
| `path.dirname(path)` | returns the directory name of a path | `'/home/user/dir'` |
| `path.basename(path)` | returns the last portion of a path | `'file.txt'` |
| `path.extname(path)` | returns the extension of the path | `'.txt'` |

** Other useful `path` methods **

| method name | description | example use | example output |
|---|---|---|---|
| `path.normalize (path)` | normalizes the given path, resolving `..` and `.` segments | `path.normalize ('/foo/bar//baz/asdf/quux/..')` | `'/foo/bar/baz/asdf'` |
| `path.join (path)` | joins all given path segments together using the platform specific separator as a delimiter, then normalizes the resulting path | `path.join ('/foo', 'bar', 'baz/asdf', 'quux', '..')` | `'/foo/bar/baz/asdf'` |
| `path.relative (from, to)` | returns the relative path from `from` to `to` | `path.relative ('/data/orandea/test/aaa', '/data/orandea/impl/bbb')` | `'../../impl/bbb'` |
| `path.isAbsolute (path)` | determines if path is an absolute path  | `path.isAbsolute('/foo/bar')` | `true` |

Note: the default operation of the path module varies depending on the OS on which Node.js is running.

#### c) Querystring module

The querystring module is used for parsing and formatting URL query strings. It can be accessed using `require('querystring')`.

- `querystring.parse(str)` parses a URL query string into a collection of key and value pairs
``` javascript
querystring.parse('foo=bar&abc=xyz&abc=123');
// returns { foo: 'bar', abc: [ 'xyz', '123' ] }
```

- `querystring.stringify(obj)` method produces a URL query string from a given object
``` javascript
querystring.stringify({ foo: 'bar', baz: ['qux', 'quux'], corge: '' });
// returns 'foo=bar&baz=qux&baz=quux&corge='
```

The substring used to delimit key-value pairs in the query string (default `&`), and to delimit keys and values (default `=`), can be changed by providing additional `sep` and `eq` parameters in calls to `querystring.parse()` and `querystring.stringify()`.


### Investigate the request and response objects, what are some of their useful properties? (Lucy)
Request and response objects are the first and second parameters of the request handler callback. For an excellent written introduction to these objects, read [Mixu's Node Book](http://book.mixu.net/node/ch10.html)

```
//Request handler callback

var http = require('http');
var server = http.createServer(function(request, response) {
  //Handle requests here!
  });
```

#### Request object
The request object is a **readable stream** (see Streams and Event Emitters section), and it comes with a number of useful properties, including:
- request.url: a url without a server, protocol or port
  - this important property identifies which page was requested and what to do with the request
- request.method: eg GET, POST, PUT, DELETE. The two most used are
  - GET, which retrieves a resource, and
  - POST, which are generally part of form submissions
- request.header: an object on request object containing params and cookies, which can be accessed once headers are parsed
- request.body: this is important in POST and PUT requests

#### Response object
The request object is a **writable stream**. Among the interesting and useful methods of the response object are:
- response.writeHead: sends a response header that contains a status code (eg 200, 404) plus optional arguments in cluding a human-readable phrase and headers
- response.cookies: if you change the value of cookies, this will write to the client browser
- response.write: can be used to send back the (stringified) body of the response
- response.end(): completes the response

Examples of Express request and response objects:
~~~~
request = {
    _startTime:Date,
    app:    function(req,res){},
    body           :    {},
    client         :    Socket,
    complete       :    Boolean,
    connection     :    Socket,
    cookies        :     {},
    files          :     {},
    headers        :    {},
    httpVersion    :    String,
    httpVersionMajor    :    Number,
    httpVersionMinor    :     Number,
    method         :    String,  // e.g. GET POST PUT DELETE
    next           :    function next(err){},
    originalUrl    :    String,     /* e.g. /erer?param1=23¶m2=45 */
    params         :    [],
    query          :    {},
    readable       :    Boolean,
    res            :    ServerResponse,
    route          :    Route,
    signedCookies  :    {},
    socket         :    Socket,
    url            :    String /*e.g. /erer?param1=23¶m2=45 */
}

response = {
    app            :    function(req, res) {},
    chunkedEncoding:    Boolean,
    connection     :     Socket,
    finished       :    Boolean,
    output         :    [],
    outputEncodings:    [],
    req            :    IncomingMessage,
    sendDate       :    Boolean,
    shouldkeepAlive    : Boolean,
    socket         :     Socket,
    useChunkedEncdoingByDefault    :    Boolean,
    viewCallbacks  :    [],
    writable       :     Boolean
}
~~~~
[source](http://www.murvinlai.com/req-and-res-in-nodejs.html)

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
