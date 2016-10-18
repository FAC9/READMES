# CSS README

# What's the CSS box model?
Ewelina

# Responsive vs mobile-first design

# What are your options for creating a grid system? What are the pros and # cons of each?

Emily



# Pre-processors

A CSS pre-processor is simply a program which takes stylesheet-like files, processes/modifies them in some way, and outputs a valid CSS document.

There are several challenges which designers/developers offer face:
* Writing valid, readable and organised CSS can become challenging when a project grows.
* Style declarations can appear to be confusing when a component contains many sub-modules.
* Updating old rules in one giant stylesheet can be a bore.
* Large stylesheets can take the user long to download.

CSS-processors can help tackle these problems. Often a new syntax (similar to CSS) is required to an available engine, in order for the pre-processor to properly interpret the files, but the output is always .css files.

## Popular pre-processors

SASS, LESS and STYLUS and the most popular and most used pre-processors.
All three require a small amount of set up to configure a project. Command line tools are available so that the pre-processor can analyse a stylesheet file in your project, process it in some way and then create a .css file in a specified location within the project. Pre-processors can also tell you useful information about your files, and even minify them to be suitable for production use.

### Sass

Sass requires ruby to run, and files are written in .scss format. These files contain syntax very similar to .css. Sass is very popular and allows developers to use variables, functions, and nesting in rules.

Here's an example of scss syntax using variables;

```css
$font-stack:    Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

Which would compile to this;

```css
body {
  font: 100% Helvetica, sans-serif;
  color: #333;
}
```

The ability to nest rules is simplified in sass;

```css
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li { display: inline-block; }

  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}
```

Which gets compiled to this;

```css
nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}

nav li {
  display: inline-block;
}

nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}
```

Check out [sassmeister](http://www.sassmeister.com/) to view outputted sass files in the browser.

### LESS

Less is also extremely popular, and offers a slightly different syntax. Less offers more built in functions in Sass that can be used to modify style content and generate rules in a number of ways. Files are written in .less format, check out this example;

```css
.box {
  color: saturate(@base, 5%);
  border-color: lighten(@base, 30%);
  div { .box-shadow(0 0 5px, 30%) }
}
```
Compiles to this;

```css
.box {
  color: #fe33ac;
  border-color: #fdcdea;
}
.box div {
  -webkit-box-shadow: 0 0 5px rgba(0, 0, 0, 0.3);
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.3);
 }
```

Check out the [less](http://lesscss.org/) site for further info.

### STYLUS

Stylus is a pre-processor that focusses less on functional power and more on cleaner syntax. In styles, developers/designers can write cleaner code by ommitting curly braces, semi-colons, variables etc.

For example;

```
body
  font: 12px Helvetica, Arial, sans-serif

a.button
  border-radius: 5px
```

Compiles to this;

```css
body {
    font: 12px Helvetica, Arial, sans-serif;
}

a.button {
    border-radius: 5px;
}
```
Check out [stylus-lang](http://stylus-lang.com/) for further info.

### When should I use a pre-processor?

It is worth exploring all three pre-processors, following online tutorials and examples to see if it would help you in a project. It may feel daunting at first to set up another layer to your project, but for larger projects which already implement tools for processing other types of files a CSS pre-processor can be a valuable addition.

### When should I not use a pre-processor?  

Perhaps your project is small; a simple static website with minimal styles needed. A pre-processor may not be necessary. Either way, explore what options are available and what works best for you.
