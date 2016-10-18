# DOM manipulation

This README outlines the basic principles of DOM manipulation:

__1. Explain the phrase 'DOM manipulation is expensive'. How can we make it more efficient?__

__2. How can we use DOM element relationships to access elements?__

The DOM hierarchy consists of different types of nodes which correspond to different 'components' of the DOM interface. We are able to access, in other words, select one or more nodes so that we can manipulate them.

The five most common ways to access DOM elements/nodes are as follows:

  * By ID

  `document.getElementById("id_name")`
  * By Class

  `document.getElementsByClassName("class_name")`

  * By Tag Name

  `document.getElementsByTagName("tag_name")`

  * By query selector

  `document.querySelector("selector");`

  * By query selectors

  `document.querySelectorAll("selector1, selector2")`

However, the DOM nodes are related to each other and we can take advantage of these relationships to access nodes based on their relationships with other nodes, as follows:

  * Selecting child nodes of a given node ([elementNodeReference])

  `[elementNodeReference].childNodes;`

  * Selecting the first or last child of a given node

  `[elementNodeReference].firstChild;`
  `[elementNodeReference].lastChild;`

  * Selecting the previous or next sibling of a given node

  `[elementNodeReference].previousSibling`  
  `[elementNodeReference].nextSibling`

  * Selecting the parent node, i.e. the node that encloses a given node

  `[elementNodeReference].parentNode`

It is worth noting that many of the DOM methods that are presented above return HTMLCollections which are array-like objects of the selected nodes (in document order). However, the `getElementById()`, `firstChild`, `lastChild`, `previousSibling`, `nextSibling`, and `parentNode` methods return a single node, as their name suggests.  

__3. What is a node in the DOM? What different types of node are there?__

__4. How can we use DOM manipulation to dynamically change the content and style of HTML elements?__

### Resources
* [Tuts+](https://code.tutsplus.com/tutorials/javascript-and-the-dom-series-lesson-1--net-3134)
* [callmenick.com](http://callmenick.com/post/basics-javascript-dom-manipulation)
* [dom-tutorials](https://dom-tutorials.appspot.com/static/index.html)
