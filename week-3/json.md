# JSON Objects

## What are JSON objects

### Key characteristics

### Usage

## How are they different from 'normal' objects?

The syntax of JSON was inspired by the JavaScript Object Literal notation, but there are differences between them.

For example, in JSON all keys must be quoted, while in object literals this is not necessary:
```javascript
// JSON:
{ "foo": "bar" }

// Object literal:
var o = { foo: "bar" };
```
Formatting property names to strings is essential, it prevents property names from accessing JavaScript reserved keywords ...
```javascript
var o = { if: "foo" }; // SyntaxError
```

Only double quotes are allows when using property/values:
``` javascript
{ "foo": 'bar' } // Invalid JSON
```

In JavaScript objects, you can display numbers as Hexadecimal Literals (e.g. 0xFF) or Octal Literals (e.g. 010), whereas in JSON you can only display decimal numbers:
```javascript
{ "foo": 0xFF } // Invalid JSON
```

JavaScript objects allow for a variety of value types to be stored (functions, sets, arrays etc).
In JSON, the data types allowed are limited to the following:
- string
- number
- object
- array
- true
- false
- null

There are a number of resources online available to validate JSON, for example [JSLINT](http://jsonlint.com/#) offers syntax highlighting to help analyze issues in JSON files.

### Converting between them

JSON objects are stored in a single string:
```javascript
var json = '{"name":"nick", "age":27}';
```
So in order to parse them to use as real objects, you can use JSON.parse():
```javascript
var json = '{"name":"nick", "age":27}';
    json = JSON.parse(json);
console.log(typeof json == "object") // true
console.log(Object.keys(json)) // [name, age]
```
To convert an object to JSON, you can use JSON.stringify:
```javascript
var obj = {
    name: "nick",
    age: 27
}
    obj = JSON.stringify(obj);
console.log(typeof obj == "string") // true
console.log(obj) // '{"name":"nick", "age":27}'
```

### Resources

[JSON.parse](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse)

[JSON.stringify](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)
