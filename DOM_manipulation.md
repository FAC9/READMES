#This is DOM manipulation README

## How can we use DOM manipulation to dynamically change the content and style of HTML elements?


The Document Object Model (DOM) provides a structured representation of the document. It defines a way that the structure can be accessed from programs so that they can change the document structure, style and content.

The DOM is also referred to as an API. Yes thats right...

* The DOM API allows the **interaction** and **manipulation** of the html document in the browser through Javascript code.

* To dynamically change the content and style of HTML elements we must first access the respective elements.

### We must first learn how to *access* the desired nodes

Finding a node on a page is the most fundamental task when working with the DOM from JavaScript.

1. **Find node by Id/Class:**
```javascript
document.getElementById
document.getElementsByClassName
```
Sometimes the node you want to manipulate does not have an ID. This is particularly true of text nodes, which can't have IDs.
Each node has a childNodes property that contains an ordered array of all its children. This can be extended to sibling and parent relationships to select the desired node.
```javascript
document.getElementById().childNodes[?]
```
2. **querySelector and querySelectorAll:** <br />
<br />
querySelector uses the CSS selector syntax. ```querySelector``` will match the *first* match only, whereas ```querySelectorAll``` will return *all* matches.
Syntax:
```javascript
document.querySelector("< CSS selector >")
```

### Once we've accessed the desired nodes we can *dynamically change* the content and style

##### Changing the DOM 
The *simplest* way to to change the DOM is to assign some HTML to an element's textContent property. This will erase the element's current content and replace it with your own. Eg.

```javascript
element.textContent = "Hello World!"
```

##### Event triggered manipulations

To make DOM manipulations dynamic we use event triggered actions, aka we need a user interaction to tell the code to run! There are a great number of event calls.

"The eventListener method can be attached to an element. This method takes two arguments - an event, and a function. The listener will wait for the specified event to occur, at which point the second argument - the function, will be executed." Syntax:

```javascript
element.addEventListener("event", function)
```

Eg.
```javascript
var foo = document.getElementById('id');

foo.addEventListener('click', function() {
  this.style.background = '#ff8';
  });
  ```

  *This document is unfinished, please feel free to refine* :)
