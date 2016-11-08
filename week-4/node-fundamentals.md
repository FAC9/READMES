# Node fundamentals
Create a readme on the methods and properties you find most useful for the group to know.

### Investigate the core modules: http, fs, and their methods. (Peter)

Create a readme on this topic

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
|---|---|---|
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
Create a readme on this topic

### Look into module.exports. How does it work (Nori)
Create a readme on this topic
