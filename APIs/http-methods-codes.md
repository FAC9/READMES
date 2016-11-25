
###HTTP Methods

####GET

This is, funnily enough, used to 'get' or retrieve resources such as HTML, JavaScript, CSS, images and so on. As a general rule, `GET` requests should not modify the resource in any way (i.e. they are 'idempotent', see above for further details).

####POST

This method may be familiar from writing forms. `POST` is used to send data to the server. The resource at the path specified in the request will deal with the data. The data is sent in the body of the request with the encoding method specified in an additional header called `Content-Type` so that the server knows how to decode the information. A `Content-Length` header is also required so that the server knows when it has received all of the information (a large amount of data might be split across multiple requests).

The response code `201: Created` indicates that the resource has been created but browsers might not 'take the hint' and redirect to the resource, so you may prefer to explicitly return a redirect code.

####PUT

`PUT` places some provided data at the exact path specified in the request. If something already exists at that path the server will replace whatever is there.

Note the distinction between `PUT` and `POST`: with `POST` the path specified in the request will handle the data and the server can put the data where it likes. A `PUT` request is basically a request to update the resource at the specified path with the data provided.

The server should respond with a `200` or `204` response if the resource was updated successfully.

####HEAD

This is the same as `GET`, except the response only includes the status code and headers. Any resource requested is not actually provided in response. This may be useful in certain circumstances as it allows you to check the validity of the path without actually having to send the resource.

####DELETE

An obvious one - the client has requested the server to delete the resource at the path specified. This is useful in RESTful APIs, but obviously you will want to check that the user is authorised to delete the resource.

A `200` or `204` response indicates that the resource was successfully deleted.

####TRACE

The server will return the request message in the response. Used for debugging.

####OPTIONS

The client is requesting information about available ways of communicating with the server about the specified resource.

You are most likely to encounter such requests as 'preflight' requests. This happens when the client will send an `OPTIONS` request to a server to determine whether it is safe to send the actual request. For example, cross-site requests require preflighting in this way.

####CONNECT

For use with proxies, not relevant to us.

####PATCH

`PATCH` should be used to upate partial resources e.g. updating a single field in a resource (where using `POST` would replace the entire resource with the single field provided). Most relevant for use as part of a RESTful API.

###Status codes

You will have noticed that the example response above included a status code. They are usually accompanied by a human-readable phrase e.g. `200 OK`. There are many status codes, so don't expect to have to know them all, but it is useful to know how they are split into different groups and the main ones from each group.

####1xx

These are known as 'informational' codes, indicating that the request was received and a provisional response has been supplied.

#####100 Continue

The server has received and approved the request headers and giving permission to the client to send the request body. This is useful when the client wants to post a large amount of data. The client first sends the headers. The server validates the headers and if it is content to receive the data sends the `100 Continue` response.

#####101 Switching Protocols
The requester has asked the server to switch protocols and the server has agreed to do so

####2xx

These are success codes, indicating that the request was received and correctly processed :blush:.

#####200 OK

All is well. If a resource was requested it will be provided.

#####201 Created

The request has been fulfilled and a new resource has been created. Its location is specified in a `Location` header or the request URL itself.

#####202 Accepted
The request has been accepted for processing, but the processing has not been completed. The request might or might not be eventually acted upon, and may be disallowed when processing occurs.

#####203 Non-Authoritative Information (since HTTP/1.1)
The server is a transforming proxy (e.g. a Web accelerator) that received a 200 OK from its origin, but is returning a modified version of the origin's response.

#####204 No Content

The request has been fulfilled and the server has no response body to send (headers will be sent). This could be used in a web app to indicate that an action was completed without navigating away from the current page.

####3xx

These indicate some kind of 'redirection'.

#####300 Multiple Choices
Indicates multiple options for the resource from which the client may choose (via agent-driven content negotiation). For example, this code could be used to present multiple video format options, to list files with different filename extensions, or to suggest word-sense disambiguation.

#####301 Moved Permanently

The requested resource has been moved to a new URL. The client's browser should use the enclosed URLs when requesting this resource in future. Note that if this is given in response to a `POST` request, for 'historical reasons' browsers will generally switch to a `GET` method when following the redirect.

#####302 Found

A temporary redirection. Future requests may continue using the original URL, not the temporary one returned in the request. As with `302`, browsers are liable to change the original request method on redirect.

#####303 See Other

This is primarily intended for responding to `POST` requests. Remember that a server may respond to a `POST` request by storing the resource wherever it wants. It provides a `303 See Other` response to let the client know the resource's URL so that the user may bookmark it etc.

#####304 Not Modified

This is used along with caching headers to indicate that the resource has not been modified and the client's cached version should be used.

#####307 Temporary Redirect

This status code is similar to `302` but corrects the error that browsers may switch HTTP methods. A client browser may not switch method to follow a `307` redirect.

#####308 Permanent Redirect

As with `307`, this is similar to `301` but browsers may not switch methods.

####4xx

These codes indicate some kind of error with the request.

#####400 Bad Request

The server cannot or will not process the request due to an apparent client error (e.g., malformed request syntax, too large size, invalid request message framing, or deceptive request routing).

#####401 Unauthorized

The request needs to be authenticated. The response will include a `WWW-Authenticate` header specifying how to authenticate.

#####403 Forbidden

The server understood what you requested but refuses to authorise it. It may give the reason in the response payload but it is not required to.

#####404 Not Found

The famous one! The client has requested a resource that the server doesn't know how to find.

#####405 Method Not Allowed
A request method is not supported for the requested resource; for example, a GET request on a form which requires data to be presented via POST, or a PUT request on a read-only resource.

#####406 Not Acceptable
The requested resource is capable of generating only content not acceptable according to the Accept headers sent in the request.

#####408 Request Time-out
The server timed out waiting for the request.

#####411 Length Required
The request did not specify the length of its content, which is required by the requested resource.

#####412 Precondition Failed
The server does not meet one of the preconditions that the requester put on the request.

#####413 Payload Too Large
The request is larger than the server is willing or able to process. Previously called "Request Entity Too Large"

#####414 URI Too Long
The URI provided was too long for the server to process. Often the result of too much data being encoded as a query-string of a GET request.

#####418 I'm a Teapot
Any attempt to brew coffee with a teapot should result in the error code `418 I'm a teapot`. The resulting entity body MAY be short and stout.

#####426 Upgrade Required
The client should switch to a different protocol such as TLS/1.0, given in the Upgrade header field.

#####429 Too Many Requests

The server is rate-limiting the client's requests and too many have been sent. The server may optionally provide a `Retry-After` headers saying how long to wait.

#####431 Request Header Fields Too Large
The server is unwilling to process the request because either an individual header field, or all the header fields collectively, are too large.


####5xx

This group of responses indicates an error with the server.

#####500 Internal Server Error

The server has encountered a problem and can't fulfil the request. Normally this happens if the route handler has a bug in it.

#####502 Bad Gateway
The server was acting as a gateway or proxy and received an invalid response from the upstream server.

#####503 Service Unavailable

The server can't deal with your request due to temporary overload or scheduled maintenance. It might respond with a `Retry-After` header to let the client know how long to wait.

#####508 Loop Detected
The server detected an infinite loop while processing the request (sent in lieu of 208 Already Reported).
