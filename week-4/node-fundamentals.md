# Node fundamentals
Create a readme on the methods and properties you find most useful for the group to know.

### Investigate the core modules: http, fs, and their methods. (Peter)
Create a readme on this topic

### Investigate the core modules: url, path, querystring, and their methods. (Marko)
Create a readme on this topic

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
Create a readme on this topic
