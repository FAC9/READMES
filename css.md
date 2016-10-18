# CSS README

# What's the CSS box model?
Ewelina

# Responsive vs mobile-first design

# What are your options for creating a grid system? What are the pros and # cons of each?

## What is a grid system?

A grid system is a way of organising content on a web page. A grid is usually made up of the following:
* A container (in which all other elements are placed)
* Columns
* Rows
* Gutters (the space between columns)

![Sample grid courtesy of The Grid System](http://www.thegridsystem.org/wp-content/uploads/2015/12/thatEmil-flexbox-grid.png "CSS Grid example")

Grids are typically divided into 12 columns. This is designed to me optimised for a desktop screen. On smaller screens, like a phone, the columns get stacked on top of one another.

Here are some advantages to using a grid to structure a web page:
* Once you've got your grid set up, it's relatively easy to make changes
* Easy to keep pages responsive
* More flexibility than the likes of flexbox when dealing with a lot of content on one page

Here's another example of what a grid might look like:
![Sample grid courtesy of Site Point](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2013/05/960-12-col-grid.jpg)

## Ways of using the grid system

### 1: Use a framework

Frameworks come with all the styling and CSS readily set up for you. The most commonly used framework for grid systems is probably [Bootstrap](http://getbootstrap.com/).

#### Pros of Bootstrap:
* Easy to set up
* Make responsive websites quickly and easily
* Big, active community and lots of support
* Nice sleek design

#### Cons of using Bootstrap (or other framework):
* If you just want a simple grid layout, it's a bit over the top. It comes with lots of other features / styles included.
* Could clash with existing styles.
* No frameworks at FAC ;)

### Make your own
You can make your own simple grid by organising your content (i.e. columns and rows) into divs and applying a max-width to each column with CSS.

A really simple grid might look like this:

```
<!DOCTYPE html>
<div class="grid">
  <div class="col-2-3">
     Main Content
  </div>
  <div class="col-1-3">
     Sidebar
  </div>
</div>

```

```
.col-2-3 {
  width: 66.66%;
}
.col-1-3 {
  width: 33.33%;
}
```

#### Pros of making your own grid
* You have full control

#### Cons of making your own grid
* It takes longer to set up that a framework

### CSS Grid Layout

Grid is a new feature of CSS. It's a W3C Working Draft, which means it currently doesn't have (much) browser support and isn't yet ready to be used in production.

With Grid you can set an element's CSS ```display``` property to ```grid``` or ```ìnline-grid```. You can then set your grid up much more easily than with the above method.

If you want to use grid, there are ways to test it in Chrome, Firefox and IE.

#### Pros of CSS Grid
* Seems to be very cool

#### Cons of CSS Grid
* It's not ready for real life applications yet!

Here's a final picture

[Pic from CSS tricks](https://cdn.css-tricks.com/wp-content/uploads/2016/03/grid-template-areas.png "Grid example")

## Read More
[CSS Grid](https://css-tricks.com/snippets/css/complete-guide-grid/)
[W3Schools Responsive web design](http://www.w3schools.com/css/css_rwd_grid.asp)
[Creating your own grid](http://j4n.co/blog/Creating-your-own-css-grid-system)
[More about creating your own grids from CSS Tricks](https://css-tricks.com/dont-overthink-it-grids/)







# What's a CSS preprocessor? Why would you use one?
