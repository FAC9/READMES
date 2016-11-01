## What is an HTTP request?

## Background

Browsing the web is all about accessing documents that aren't sitting directly on your own computer.

As a user, all you need to know is the URL - the address of the location where that document lives. You type this address into your browser, so that you browser knows where to look. The magic happens between you typing in the URL and the document appearing on your screen.


### The magic

All you have done so far is given your browser the address. Your browser still can't access the file. It still has to knock on the door and ask for the relevant document for you. So there needs to be someone listening for that knock on the door - that's the job of the web server.

An HTTP request is like your browser knocking on the door and telling the web server what it is looking for.

The server will give your browser a response, which includes the document itself and any information that your browser needs about how to display the information to you (e.g. the file type).

## So what is HTTP?

These requests and responses are sent in a standard form defined by the _HyperText Transfer Protocol (HTTP)_. This only defines what the web browser and server say to one another.

The movement of the actual bytes themselves across the network is handled by TCP/IP, but we won't be talking about that here. For a broader explanation of each stage of the process, read [How does the Internet work?](http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm)

## Requests and responses

An _HTTP request_ is a message sent from a client to a server. A message sent from the server to the client is an _HTTP response_.

Each request message consists of:

- A _start line_, which contains three elements separated by spaces:
  - The _request method_, which describes the type of action being requested of the server.
  - The _request target_, which indicates what the method should be performed on - often a URL.
  - The _protocol name and version_ - usually "HTTP/1.0", although "HTTP/1.1" and "HTTP/2" see some use.
- (Optional) One or more _header lines_.
  - Each header line is in the form 'keyword: value', and specifies a parameter of the request.
- A _blank line_, which indicates to the server that there are no more header lines in the request.
- (Optional) A _message body_, which includes any additional data required as part of the request.

### Request methods

The most commonly used methods for an HTTP request are _GET_ and _POST_.

- The _GET_ method is used to request a particular file or resource from the server. If a GET request requires a query string, this is included as part of the URL within the request target.

- The _POST_ method is often used to pass form data to a server, but can also be used for messages that require more security than is possible with _GET_. Unlike GET requests, POST requests carry query strings in the message body, and the parameters aren't stored in browser history or web server logs.

Other methods include _HEAD_, which returns HTTP headers but no document body; _PUT_, which is used to upload data to the server; _DELETE_, which deletes the specified resource; and _OPTIONS_, which returns the HTTP request methods that the server supports.

### Example HTTP exchange

```
GET /path/file.html?value=foo HTTP/1.0   
From: someuser@jmarshall.com  
User-Agent: HTTPTool/1.0  
[blank line]
```

- Line 1: start line.
  - Method: GET. Tells the server that the client is requesting a resource.
  - Target: The URL of the requested resource, including any parameters in keyword/value pairs.
  - Protocol name and version. Tells the server that the message is using the 1.0 version of the HTTP protocol.
- Lines 2 and 3: header lines.
  - Each keyword/value pair passes a parameter about the client or the request to the server.
- Line 4: blank line.
  - This indicates that the header section has ended.

Note that the GET request has no message body, as all the information required is included in the start line and head.

### Making an HTTP request in JavaScript

First, create a new HTTP request object using ```var foo = new XMLHTTPRequest()```.

Define the request's method and target by passing them to the request object's ```open``` method as the first and second arguments, respectively: ```foo.open('GET', 'http://www.google.com')```.

If necessary, set any keyword/value pairs in the header using the request object's ```setRequestHeader(keyword, value)``` method.

Send your request using the request object's ```send``` method, including the message body as an argument if necessary.

### Resources

- [How does the Internet work?](http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm)
- [HTTP/1.1 Message Syntax and Routing](http://www.rfc-editor.org/rfc/rfc7230.txt)
