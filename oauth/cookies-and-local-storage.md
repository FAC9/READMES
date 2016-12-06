# What are cookies, how do you create, transport, access and expire them?
  Cookies are a way of storing certain information about a users session on the client machine.
  They can be set in various ways, depending on the way your server is set up, and will be automatically be returned by the client on future requests.
  Cookies can be set to expire at a certain date.

# What do you need to do in Hapi to set a cookie?
  We can simply set state when we reply 
  
```
      //set the server's cookie details
      
      server.state('nameCookie', {
      ttl: 360000,
      isSecure: false,
      isHttpOnly: false,
      encoding: 'base64json',
      clearInvalid: false,
      strictHeader: true,
      path: "/"
    });

      //call .state method on reply to set a cookie
      
     reply.file('./public/views/index.html').state('nameCookie', {name: cookieName})
```


# How do you get a cookie from a request in Hapi?
  
  We can access the cookie using request.state.nameCookie (where nameCookie could be whatever the cookie's name is) in our handler function.
  
# Briefly describe Local Storage and Session Storage (browser api)?
"The Web Storage API provides mechanisms by which browsers can store key/value pairs, in a much more intuitive fashion than using cookies."

Session storage:
- separate storage per window (or tab in browsers like Chrome and Firefox) that is available for as long as the browser is open, including page reloads and restores
Local storage:
- storage that persists until explicitly deleted, even when the browser is closed and reopened

[Getting started with localStorage vs sessionStorage in html5](http://javascript.tutorialhorizon.com/2015/09/08/getting-started-with-localstorage-vs-sessionstorage-in-html5/)
[Knowing when to use each type](https://github.com/FAC9/READMES/blob/master/hapi/cache-and-cookies.md#when-to-use-sessionstorage)
# If using Local Storage to store your users access_token, how do you transport the token to and from your server?
  Local storage allows you to save simple key value pairs on the client machine. This is a good way to improve your sites performance, and to minimise the number of requetss that are made to your server. We can save our access tokens in local storage.
  
  Because local storage is only accessible through client side Javascript, it poses some problems if we choose to store access tokens in it. Unlike cookies, which can be sent along with a the clients inital request, to use our locally stored access tokens
  
  - client must request page from server
  - client recieves and loads page
  - client accesses token from local storage, then make another request to server including this token
  - Server recieves this request with token, and then makes a request to the OAuth provider
  - OAuth provider Recieve's the token, then sends request information to our server
  - Server recieves this information, then repackages it and sends it to the client
  - The client interprets the data and updates the page accordingly.
  
  This process is much more involved than using cookies, and is somewhat clumsy... There may be situations where this is better. For example in a one page app we may want to show something, anything, to the client AS SOON AS POSSIBLE. If we use this method we can immediately show them a blank page with no data, and then update it as soon as possible... :)
