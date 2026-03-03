# CSS Specificity
- CSS Specificity determines **which CSS rule is applied** when multiple
rules target the same element.
- CSS follows this priority order:
1.  `!important`
2.  Inline styles
3.  ID selectors
4.  Class / Attribute / Pseudo-class selectors
5.  Element / Pseudo-element selectors
6.  Source order (last rule wins if specificity is equal)

-------------------------------------
## Examples

### Element Selector
``` css
div {
  color: red;
}
```
Specificity = 1

### Class Selector
``` css
.box {
  color: blue;
}
```
Specificity = 10

### ID Selector
``` css
#main {
  color: green;
}
```
Specificity = 100

### Inline Style
``` html
<div style="color: orange;"></div>
```
Specificity = 1000

------------------------------------------------------------------------

## Combined Selectors
``` css
div.box {
  color: red;
}
```
Specificity: - div = 1 - .box = 10 Total = 11

------------------------------------------------------------------------

## Multiple Classes
``` css
.box.active {
  color: purple;
}
```
Specificity = 10 + 10 = 20

------------------------------------------------------------------------

## Equal Specificity Rule
If specificity is equal, the **last declared rule wins**.
``` css
.box { color: red; }
.box { color: blue; }
```
Final color = blue

------------------------------------------------------------------------

## !important Rule
``` css
.box {
  color: red !important;
}
```
-   Overrides normal specificity.
-   Avoid overusing it.
-   Use only when absolutely necessary.

------------------------------------------------------------------------

# Header Meta Tags
These tags go inside the `<head>` section of HTML.
## 1. Character Encoding
``` html
<meta charset="UTF-8">
```
Defines character encoding. Always include this.

------------------------------------------------------------------------

## 2. Viewport (Responsive Design)
``` html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```
Essential for responsive websites.

------------------------------------------------------------------------

## 3. Page Description (SEO)
``` html
<meta name="description" content="Learn CSS and HTML in detail.">
```
Used by search engines.

------------------------------------------------------------------------

## 4. Keywords (Less Important Today)
``` html
<meta name="keywords" content="CSS, HTML, Grid, Flexbox">
```
Mostly ignored by modern search engines.

------------------------------------------------------------------------

## 5. Author
``` html
<meta name="author" content="Name">
```

------------------------------------------------------------------------

## 6. Compatibility Mode
``` html
<meta http-equiv="X-UA-Compatible" content="IE=edge">
```
Used for older Internet Explorer compatibility.

------------------------------------------------------------------------

## 7. Title Tag
``` html
<title>My Website</title>
```
Appears in browser tab and search results.

------------------------------------------------------------------------

## 8. Favicon

``` html
<link rel="icon" href="favicon.ico">
```
Adds icon to browser tab.

------------------------------------------------------------------------

## 9. Open Graph (Social Media Sharing)
``` html
<meta property="og:image" content="image.jpg">
```
Used for link previews on social platforms.

------------------------------------------------------------------------

# Sample Head Template
``` html
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Website description">
  <title>My Website</title>
  <link rel="icon" href="favicon.ico">
</head>
```
