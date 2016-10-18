# CSS README

# What's the CSS box model?

All HTML elements can be considered as boxes. In CSS, the term "box model" is used when talking about design and layout.

According to the box model concept, every element on a page is a rectangular box and may have width, height, padding, borders, and margins.

The box model is the specification that defines how a box and its attributes relate to each other. In its simplest form, the box model tells browsers that a box defined as having width 100 pixels and height 50 pixels should be drawn 100 pixels wide and 50 pixels tall.

![alt text](images/box.png)

**Working with the Box Model**

Every element is a rectangular box and has a content area (e.g., text, an image), and there are several properties that determine the size of that box. The core of the box is defined by the `width` and `height` of an element, which may be determined by the display property, by the contents of the element, or by specified width and height properties. `padding` and then `border` expand the dimensions of the box outward from the element’s width and height. Lastly, any `margin` we have specified will follow the border.

Let’s look these properties inside some code:

```
div {
  border: 6px solid #949599;
  height: 100px;
  margin: 20px;
  padding: 20px;
  width: 400px;
}

```

When we set the width and height properties of an element with CSS, we just set the width and height of the content area.
To calculate the full size of an element, we must also add padding, borders and margins.

According to the box model, the **total width** of an element can be calculated using the following formula:

```
margin-right + border-right + padding-right + width + padding-left + border-left + margin-left
```

In comparison the **total height** of an element can be calculated using the following formula:

```
margin-top + border-top + padding-top + height + padding-bottom + border-bottom + margin-bottom
```
![alt text](images/box-model.png)

Using the formulas, we can find the total height and width of our example code.

```
Width: 492px = 20px + 6px + 20px + 400px + 20px + 6px + 20px
Height: 192px = 20px + 6px + 20px + 100px + 20px + 6px + 20px
```

If `padding` or `borders` are undeclared, they are either zero or the browser default value.

If the `width` of a box is undeclared (and the box is a **block level element**), things get a little weirder:

1. If the box has static or relative positioning, the width will remain 100% in width and the padding and border will push inwards instead of outward.
2. If the box has absolute position, the width is only as wide as it needs to be to hold the content. So if the box contains a single word, the box is only as wide as that word renders. If it grows to two words, it'll grow that wide.
3. The same exact behavior is seen with floated elements with no widths. The box is only as wide as it needs to be to accommodate the content, up to as wide as its parent element (doesn't need to be relatively positioned though).

**Inline elements are boxes too.**

We can think of them as really really long and skinny rectangles, that just so happen to wrap at every line. They are able to have margin, padding, borders just like any other box.

# Responsive vs mobile-first design
Esraa

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
