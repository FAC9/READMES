# DOM manipulation

## 1. Explain the phrase 'DOM manipulation is expensive'. How can we make it more efficient?

Almost every time that you manipulate the DOM using JavaScript, the browser needs to reflow - a process where the positions and geometries of some or all of the page content will be recalculated in order to re-render elements of the document.

If you iterate over several elements and manipulate each one separately, the DOM is forced to reflow each time. This is hard work for the browser, and will make your website appear sluggish and unresponsive. This is particularly problematic on mobile browsers.

Additionally, interacting with the DOM is far more costly than performing arithmetic operations, as queries require the browser to traverse a complex tree structure to find elements. If your DOM manipulation relies on these queries, it may affect performance - particularly when using nested loops.

Several techniques that can reduce the number of times the browser interact with the DOM or reflow:

- **Try to keep your DOM tree as shallow as possible**. Changes at any level of the tree can force the browser to reflow both up and down the tree; the deeper the tree, the more nodes the browser will need to reflow following a change.

- Where possible, **remove elements from the document flow** by using ```position: fixed``` or ```position: absolute```. Fixing the position of an element prevents it from being reflowed.

- If inserting multiple elements into the DOM, don't add them one at a time. Instead, **create a list containing each of the elements and insert it into the DOM in a single operation**. It's even faster to append an HTML string to the document directly.

- When updating complex nodes like tables, **clone the entire node and perform all of your updates in the cloned node outside of the DOM**, then replace the node in a single operation.

- Instead of manipulating multiple CSS properties of a class directly using JavaScript, **add or remove entire classes to elements to update how they're styled**.

- Rather than deleting nodes from the DOM with ```removeChild``` , hide the affected elements (```element.style.visibility = 'hidden'``` or ```element.style.display = 'none'```).  

- Similarly, rather than adding elements to the DOM using JavaScript, you can **pre-populate your page with hidden nodes and unhide them as you need them**.

- NodeLists (such as the arrays returned by ```document.getElementsByTagName```) are live objects - they are updated every time the underlying document changes, making them memory- and CPU-intensive. Instead of assigning them to a variable and iterating over the variable, **access the NodeList directly** (for example, ```for (var i = 0; (p = document.getElementsByTagName("P")[i]); i++)```).

### Additional resources

- [Google Developers - Minimising browser reflow](https://developers.google.com/speed/articles/reflow)
- [Kory Nunn - The DOM isn't slow, you are](https://korynunn.wordpress.com/2013/03/19/the-dom-isnt-slow-you-are/)
- [Stoyan Stefanov - Rendering: repaint, reflow/relayout, restyle](http://www.phpied.com/rendering-repaint-reflowrelayout-restyle/)
- [Craig Buckler - 10 Ways to Minimise Reflows and Improve Performance](https://www.sitepoint.com/10-ways-minimize-reflows-improve-performance/)
