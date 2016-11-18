## Templating

### What is a templating engine and why would you use it? (group1)

### What is Handlebars.js? (group1)
- Superset of moustache

### Example walkthrough... (group 2 does this)

### Additional - What are the advantages of using server side rendering vs rendering dynamic content on the client? (group 1)

### Additional -  How would you use Hapi's views interface to serve dynamic content? (real life example) (group 1)


### Example

- examples of view engines (e.g. jade, handlebars. esx etc)
- Vision adds view methods
- The views method is used to configure
- Views takes a single argument with is object containing engines key which is itself an object- a mapping of file extensions to view engines (e.g. 'html: require('handlebars')... ') hbs?.
- Views needs a path of where to find views, 'relateTo: "__dirname"' (directory of where views located), and path, which is relative to the directory (e.g. views).
- All of these steps are rquired before adding routes to serve the views
- inside the handler, the view method is added to the reply object ()
- view takes a first name as the view method (e.g. home, no need for home.html if view engine set for html).
- HBS files use {{ }} syntax...
- optional path parameters can be added in the path . e.g. '/{name?}', the name parameter will be available in the params object in the request object.
- reply.view('home', { name: request.params.name || world, }).
- By setting layout to true, you can create a layout file (e.g. layout.hbs), which uses {{{content}}} as the placeholder view
