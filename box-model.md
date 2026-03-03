# CSS Box Model?
- In HTML + CSS, every single element is a rectangular box.
- Whether it is:
```html
1. <div>
2. <p>
3. <h1>
4. <button>
5. <img>
```
- Everything is treated as a box.
- That box is made up of 4 layers : Content, Padding, Border, Margin
```
+-----------------------------+
|           Margin            |
|   +---------------------+   |
|   |       Border        |   |
|   |   +-------------+   |   |
|   |   |   Padding   |   |   |
|   |   |  +-------+  |   |   |
|   |   |  |Content|  |   |   |
|   |   |  +-------+  |   |   |
|   |   +-------------+   |   |
|   +---------------------+   |
+-----------------------------+
```
------
### Content
This is the actual stuff inside the element.
Example:
```css
<div class="box">
  Hello World
</div>
.box {
  width: 200px;
  height: 100px;
}
```
Here:
width: 200px
height: 100px

------
### Padding
Padding is the space between content and border.

It is inside the element.

```css
.box {
  width: 200px;
  height: 100px;
  padding: 20px;
}
```
Now The total visible size becomes:

Width = 200 + 20(left) + 20(right) = 240px
      
Height = 100 + 20(top) + 20(bottom) = 140px

So padding increases the actual size.
```css
/*Padding Shorthand*/
padding: 20px;        /* all sides */
padding: 10px 20px;   /* top/bottom  left/right */
padding: 10px 15px 20px 25px; /* top right bottom left */

padding-top: 10px;
padding-right: 20px;
padding-bottom: 10px;
padding-left: 20px;
```

------
### Border
Border wraps around padding + content.
```css
.box {
  border: 5px solid black;
}
```
Now total width becomes:

Width = content + padding + border
      = 200 + 40 + 10
      = 250px
```css
/*Shorthand:*/
border: 5px solid red;

border-width: 5px;
border-style: solid;
border-color: red;

```
-----
### Margin

Margin is space outside the element.

It creates space between elements.
```css
.box {
  margin: 20px;
}
```
This does NOT increase background area.
It only pushes the element away from others.
```css
/*Margin Shorthand*/
margin: 20px;
margin: 10px 20px;
margin: 10px 15px 20px 25px;
```
-----

Example:
```css
.box {
  width: 200px;
  height: 100px;
  padding: 20px;
  border: 5px solid black;
  margin: 10px;
}
```
Actual total width on screen: 200 (content) + 40 (padding) + 10 (border) + 20 (margin) = 270px

Actual total height: 100 + 40 + 10 + 20 = 170px

## box-sizing :

CSS uses:
```css
box-sizing: content-box;  /*  width = only content*/
```
This creates layout issues because padding and border increase size unexpectedly.

So we can use:
```css
box-sizing: border-box;
```
With this, width includes: content, padding, border. So:
```css
.box {
  width: 200px;
  padding: 20px;
  border: 5px solid black;
  box-sizing: border-box;
}
```
Now total width stays 200px only.

Content automatically shrinks to adjust.

------
-------

# Inline vs Block Elements
- Every HTML element has a default display value.
- Main types:
1. block
2. inline
3. inline-block
## Block Elements
- Starts on a new line
- Takes full available width
- Respects width and height
- Allows margin and padding on all sides

```html
COMMON BLOCK ELEMENTS
<div></div>
<p></p>
<h1></h1> to <h6></h6>
<section></section>
<article>
<header>
<footer>
<ul>
<li>
```
```css
Example :
<div class="box1">Box 1</div>
<div class="box2">Box 2</div>
div {
  color: white;
}

Result:
Box 1
Box 2
```
They appear one below the other.
Because block elements take full width.

Block Respects Width & Height
```css
div {
  width: 200px;
  height: 100px;
  background: pink;
}
```
Now it becomes 200px wide only.

## Inline Elements
- Does NOT start on a new line
- Takes only the width of its content
- Ignores width and height
- Vertical margin behaves differently

```html
Common Inline Elements
<span></span>
<a></a>
<strong></strong>
<em></em>
<label></label>
```
```html
Example
<span>Meghana</span>
<span>Learning CSS</span>
```
They appear side by side.

Suppose if we write,
```css
span {
  width: 200px;
  height: 100px;
}
```
Nothing happens.Because inline elements ignore width & height.

## Inline-Block 

This is a hybrid.
```css
span {
  display: inline-block;
  width: 150px;
  height: 50px;
  background: orange;
}
```
Appears inline (side by side) But respects width & height

This is commonly used for:
- Buttons
- Nav items
- Cards
### Changing display type:
```css
div {
  display: inline;
}
span {
  display: block;
}
```
Display is just a CSS property.

# Positioning
- CSS has 5 main position values:
1. static (default)
2. relative
3. absolute
4. fixed
5. sticky
## position: relative
- The element moves relative to its original position.
- It still occupies original space.
```css
<div class="box"></div>
.box {
  width: 100px;
  height: 100px;
  background: red;
  position: relative;
  top: 20px;
  left: 30px;
}
```
It moves 20px down, 30px right BUT its original space is still reserved

It visually shifts but layout space stays.

**Use of Relative**
- create a positioning reference for absolute children.

## position: absolute
- The element is removed from normal document flow.
- It positions itself relative to:
- The nearest positioned ancestor
(ancestor with relative, absolute, fixed, or sticky)
- If none exists, It positions relative to the <body>.
```css
<div class="child"></div>
.child {
  position: absolute;
  top: 0;
  right: 0;
}
```
It goes to top-right of page.
## Absolute Inside Relative
```css
<div class="parent">
  <div class="child"></div>
</div>
.parent {
  width: 300px;
  height: 300px;
  background: lightgray;
  position: relative;
}

.child {
  width: 100px;
  height: 100px;
  background: red;
  position: absolute;
  top: 0;
  right: 0;
}
```
Child goes to top-right of parent because parent has position: relative.
## Z-Index
- When using absolute positioning, elements may overlap.
- Higher z-index = appears on top.
- Works only if position is NOT static.
```css
z-index: 10;
```
