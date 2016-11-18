## Templating

#### Template Engine Definition

- Software designed to combine one or more templates with a data model to produce one or more result documents.
- A main purpose is to process templates & data to output text.

Here is a diagram illustrating all of the basic elements and processing flow of a template engine:

![alt text](images/template-engine.png)

#### Benefits of using Template Engines
- Encourages good code organization (**separate model (= logic)** and **view (= presentation)**).
- Reusable templates.
- Provides a more elegant way to create dynamic DOM elements (client-side).

#### What is Handlebars.js? (group1)
- One of the most popular JavaScript templating engines.
- Not specific to Hapi or Node.js, can be used for any JS templating.
- Builds on top of Mustache templating engine.
- In Hapi, handlebars can be used as the engine for rendering `html` templates.

As in Mustache, handlebars templates look like regular HTML, with embedded placeholders (e.g. `{{expression}}`).

``` html
<body>
 <h1>{{title}}</h1>
 <section>
   {{introduction}}
 </section>
</div>
```

In Hapi, parameters that are provided by the client request are available in the `query` object.

``` html
<div>{{query.paramName}}</div>
```

Handlebars provides additional helpers (functions used within templates), such as:
- `{{#with}}` helper takes an object and then allows you to refer to its properties
- `{{#each}}` helper allows you to loop through an object's properties

To implement custom helpers, these can be provided a in separate `js` file and exported using `module.exports`. The name of each helper file will be used as the helper name in the template.

When configuring `server.views`, the `helpersPath` property is used to let Hapi know where to find our custom handlebars helpers.


### Example Guide

Here we start with a basic example of using Hapi to serve a static file, by using the the Inert plugin which is required before defining a home route;

```javascript
'use strict'
const Hapi   = require('hapi');
const server = new Hapi.Server();

server.connection({ port : 8000})

server.register(require('inert'), () => {

 server.route({
   method: 'GET',
   path: '/',
   handler: function(request, reply){
     reply.file(__dirname + '/public/index.html'));
   }
 });
})
server.start(() => console.log(`Startd at: ${server.info.uri}`))
```
A view engine can be used to render views, which represent files that are outputted to the client.
To add view support for your Hapi server, the Vision plugin needs to be registered. Vision adds template rendering support for template engines like Handlebars.
We then need to configure at least one templating engine on the server. This is done by using .views method on the Hapi server;
```javascript
//...
server.register(require('vision'), () => {

 server.views({
   engines: {
     html: require('handlebars')
   }
 })
//...
})
```
Views takes a single argument, which is an object containing engine keys (which is itself an object). The engine keys object contains a mapping of file extensions to engines. The Views method needs a path of where to find the views;
```javascript
server.views({
 engines: {
   html: require('handlebars')
 },
 path: __dirname + '/views'
})
```
You can also use the relativeTo key to set the directory instead of the whole path;
```javascript
server.views({
 engines: {
   html: require('handlebars')
 },
 relativeTo: __dirname,
 path: 'views'
})
```
Here is an example of how the file structure for a project with views would look;
```
my-project-folder
|- server.js
|- views
 |- layout.html
 |- index.html
```

With Hapi, to pass object values to views, you can call the view method in the reply object in the handler like so;
```javascript
server.route({
 method: 'GET',
 path: '/',
 handler: function(request, reply){
   reply.view('index.html', {name: 'John'})
 }
});
```
The first argument takes the file found in the views directory (configured previously, note that the '.html' is optional), the second is an object with key/value pairs to set the content in the view file. Optional path parameters can be added in the path of the route, so when the client navigates to a particular endpoint, these parameters will then be available in the request object under params;
```javascript
server.route({
 method: 'GET',
 path: '/{name}',
 handler: function(request, reply){
   reply.view('index.html', {name: request.params.name})
 }
});
```
So if the user navigates to '/timmy', and the view file is configured like this;
```html
<div>My Name Is {name}</div>
```
Then the server will combine the parameters given with the template file to output the following to the client-
```html
<div>My Name Is Timmy</div>
```
To define html data to be rendered in the view file, you can additionally use {{{}}} syntax;
```html
<!DOCTYPE html>
<html>
 <head>
   <meta charset="utf-8">
   <title>I'm hapi!</title>
   <style>
     * {
       font-family: 'Open Sans';
       font-weight: 100; color: #333;
     }
   </style>
 </head>
 <body>
   {{{content}}}
 </body>
</html>
```
Here, {{{content}}} represents other views that can be loaded into this file. This is known as templating. Layout files allow you to link view files together to minimise repetition (e.g in blog posts, where the same html head tags and styles are used for different blogs). To set a common layout file in your project, save it as a layout.html file in the views folder, then in the .views method on the Hapi server, set the layout value to true;
```javascript
server.views({
 engines: {
   hbs: require('handlebars')
 },
 relativeTo: __dirname,
 layout: true,
 path: 'views'
})
```
Now, when the user navigates to '/timmy', the handler will return the contents of index.html (with the name parameter passed in to the file) embedded with the layout.html file. So the client will receive the following;
```html
<!DOCTYPE html>
<html>
 <head>
   <meta charset="utf-8">
   <title>I'm hapi!</title>
   <style>
     * {
       font-family: 'Open Sans';
       font-weight: 100; color: #333;
     }
   </style>
 </head>
 <body>
   <div>My Name Is Timmy</div>
 </body>
</html>
```

### Advantages of using server side rendering vs rendering dynamic content on the client

**Server-side rendering**: Server renders the HTML page before sending it to the client.  
**Client-script rendering**: JavaScript running in the browser produces HTML or manipulates the DOM

Benefits of server side rendering:
- Your content is visible to search engines like Google
- The page loads faster. There is no delay between retrieving the server response and rendering the page
- It maintains the idea that pages are documents. If you ask a server for a document by URL, you get back the text of the document rather than instructions on how to manipulate the document.
- Ensures that there are few browser compatibility issues, as the server deals with the content manipulation..

Benefits of client-side rendering:
- You can update the screen instantly when the user clicks, rather than waiting for the server to respond.
- Great for animated or highly interactive content.

Note that the two are not mutually exclusive. Most websites will use both server-side and client-side rendering, with static, navigable content being rendered on the server, app-like interactivity being handled by the code running in the browser.

### Resources

- [Template engines](http://www.simple-is-better.org/template/)
- [Template processor](http://www.wikiwand.com/en/Template_processor#/Template_engine_2)
- [The top 5 JavaScript templating engines](http://www.creativebloq.com/web-design/templating-engines-9134396)
- [Hapi — Create and Use Custom Handlebars Helpers](https://futurestud.io/tutorials/how-to-create-and-use-custom-handlebars-helpers-with-hapi)
