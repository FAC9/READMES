# Cache and cookies

## Client-side storage is a minefield

Handling client-side storage well is fundamental to developing performant web apps - especially for developing progressive web apps, which rely heavily on client-side storage to function.

- Cookies: Cookies are supported by virtually every browser in circulation, and are suitable for handling session management, personalisation and tracking. They were never designed to handle general purpose client-side storage, but were often used for this purpose in the absence of any widely supported alternative. Cookies have mostly been superseded for client-side storage by other APIs (see below).
- Web Storage API: The Web Storage API  It is defined in the HTML5 standard, so should be supported by all modern browsers (although legacy browser support is patchy).
- IndexedDB: A JSON-based database API with similar functionality to NoSQL databases. It isn't part of the HTML5 standard, but it *is* recommended by W3C (the World Wide Web Consortium). It is fully supported by all modern browsers except Internet Explorer and Edge, and is partly supported by both of those.
- WebSQL: WebSQL was an attempt to incorporate SQL-style database functionality into the browser, but it was never recommended by W3C and its specification was abandoned in 2010 after Mozilla refused to support it in Firefox.

## Local storage and session storage

localStorage and sessionStorage are both browser APIs for storing data on the client side. They were introduced in the HTML5 specification and are supported by all modern browsers (although support in older browsers is patchy).

The two APIs are almost identical in their interfaces and functionality. The key difference is that sessionStorage is intended to store data for the duration of a single browser session, while localStorage is intended to store data that persists between sessions.

To put it simply, data stored through sessionStorage should be deleted when the browser window is closed. Data stored through localStorage shouldn't.

Both sessionStorage and localStorage are instances of the Storage object, one of the interfaces of the Web Storage API - a relatively recent API which provides browsers with mechanisms for storing key/value pairs.

The Web Storage API can be used in similar situations to HTTP session cookies, but offers several advantages. Unlike cookies, for example, sessionStorage is scoped to an individual window - so different windows can maintain separate state without changes in one 'leaking' into the other.

The API can also be used to store large files to improve website performance. When accessing large files and documents stored on the cloud, for example, copies may be saved in localStorage to improve load times after the initial transfer.

## When to use sessionStorage

sessionStorage creates a storage area for each origin (normally a web domain) accessed by the browser, which persists until the end of the page session.

It should be used when you need to store data on the client side temporarily. Each browser window creates its own sessionStorage instance, which is cleared when the window is closed.

## When to use localStorage

localStorage creates a separate storage area for each origin accessed by the browser, which persists until it is explicitly deleted by the user.

It should be used when data needs to be stored between sessions or for the long term, such as recording user preferences about how your website is displayed.

## Inspecting sessionStorage and localStorage

You can inspect your browser's sessionStorage and localStorage for a domain by opening Chrome's Developer Tools and selecting the Application tab.

## Using the Web Storage API

The Storage object has the following methods, which can be used on either window.localStorage or window.sessionStorage:

- Storage.key(): takes an integer as an argument, and returns the key with that index
- Storage.getItem(): takes a key name as a string, and returns that key's value
- Storage.setItem(): takes a key name and a value and adds that key to storage or, if it already exists, update its value
- Storage.removeItem(): takes a key name as a string and remove that key from storage
- Storage.clear(): removes all keys from storage (takes no arguments)
