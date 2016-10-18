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

# What are your options for creating a grid system? What are the pros and # cons of each?

Emily

# What's a CSS preprocessor? Why would you use one?
