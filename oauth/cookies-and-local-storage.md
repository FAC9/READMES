# What are cookies, how do you create, transport, access and expire them?
# What do you need to do in Hapi to set a cookie?
The [Hapi documentation](http://hapijs.com/tutorials/cookies?lang=en_US) explains how to configure the server, set cookies, overwright the options and clear cookies.

Look [here](http://hapijs.com/api#serverstatename-options) for all the available options.

This [demo](https://github.com/limeyb7/cookies-with-hapi-demo) from Hapi week is a good demonstration.

## httpOnly flag
Defaults to `true`

When you tag a cookie with the HttpOnly flag, it tells the browser that this particular cookie should only be accessed by the server. Any attempt to access the cookie from client script is strictly forbidden.

## isSecure flag
Defaults to `true`

Prevents cookies from being _observed_ by unauthorized parties due to the transmission of a the cookie in clear text (doesn't prevent them from being overwritten). Browsers which support the secure flag will only send cookies with the secure flag when the request is going to a HTTPS page.

That's why this needs to be set to `false` when you are running your website locally - you're not going to an HTTPS page.

# How do you get a cookie from a request in Hapi?

# Briefly describe Local Storage and Session Storage (browser api)?
"The Web Storage API provides mechanisms by which browsers can store key/value pairs, in a much more intuitive fashion than using cookies."

Session storage:
- separate storage per window (or tab in browsers like Chrome and Firefox) that is available for as long as the browser is open, including page reloads and restores
Local storage:
- storage that persists until explicitly deleted, even when the browser is closed and reopened

[Getting started with localStorage vs sessionStorage in html5](http://javascript.tutorialhorizon.com/2015/09/08/getting-started-with-localstorage-vs-sessionstorage-in-html5/)
[Knowing when to use each type](https://github.com/FAC9/READMES/blob/master/hapi/cache-and-cookies.md#when-to-use-sessionstorage)
# If using Local Storage to store your users access_token, how do you transport the token to and from your server?
