# **CSS Responsive Queries**
- Responsive design is making your website adjusts based on screen size.
- So, Mobile, Tablet, Laptop, Desktop
- All show optimized layout.
- Modern development prefers mobile-first because mobile constraints are stricter.
## Media Query
- Media Query lets you apply CSS only if a condition is true.
```css
@media (condition) {
  /* CSS here */
}
/* Most Common Usage — Screen Width */
@media (max-width: 768px) {
  body {
    background: lightblue;
  }
}
```
- If screen width ≤ 768px
- Apply this CSS

### Common Breakpoints 
Device |	Width
-- | --
Mobile	| 480px
Tablet |	768px
Small Laptop |	1024px
Desktop |	1200px+|

Example:
```css
/* Mobile */
@media (max-width: 480px) { }
/* Tablet */
@media (max-width: 768px) { }
/* Laptop */
@media (max-width: 1024px) { }
```
### Example: Making Layout Responsive
```css
Desktop Layout
.container {
  display: flex;
}
/* Two columns appear side by side.*/
/*For mobile:*/
@media (max-width: 768px) {
  .container {
    flex-direction: column;
  }
}
```
So, Desktop → row and Mobile → column. This is how most websites work.

# **Flexbox**
- Flexbox is a 1D layout system.
- It works in: Row OR Column
- **Step 1:** Make Parent Flex
```css
.container {
  display: flex;
}
/*Now children become flex items.*/
```
### Flex Properties (Parent)
1. flex-direction
```css
flex-direction: row;       /* default */
flex-direction: column;
flex-direction: row-reverse;
flex-direction: column-reverse;
```
2. justify-content (Main Axis)
- Controls horizontal alignment (if row).
```css
justify-content: center;
justify-content: space-between;
justify-content: space-around;
justify-content: flex-start;
justify-content: flex-end;
```
3. align-items (Cross Axis)
- Controls vertical alignment (if row).
```css
align-items: center;
align-items: flex-start;
align-items: flex-end;
align-items: stretch;
/*Example: Perfect centering*/
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
```
### Flex Item Properties (Children)
```css
.box {
  flex: 1;
}
```
- Take equal available space.
### **When to use Flexbox**
- Navbar
- Centering
- Cards row
- Buttons alignment
- Simple row/column layouts
- Flexbox = 1 dimension.

# **CSS Grid**
- Grid is a 2D layout system.
- It controls: Rows and Columns at the same time.
- **Step 1:** Make Parent Grid
```css
.container {
  display: grid;
}
```
- Define Columns
```css
grid-template-columns: 200px 200px 200px;
/*OR*/
grid-template-columns: 1fr 1fr 1fr;
```
fr = fraction of available space
- Define Rows
```css
grid-template-rows: 100px 200px;
```
### **Repeat**
```css
grid-template-columns: repeat(3, 1fr);
```
Creates 3 equal columns.
```css
.container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 20px;
}
```
This automatically:
- Adds as many columns as fit
- Each min 200px
- Expands equally
### Placing Items Manually
- Span from column 1 to 3.
```css
.item1 {
  grid-column: 1 / 3;
}
```
### Properties of container class
```css
.container {
  display: grid;

  /* Define Columns */
  grid-template-columns: repeat(3, 1fr);

  /* Define Rows */
  grid-template-rows: 100px auto 150px;

  /* Named Areas */
  grid-template-areas:
    "header header header"
    "sidebar content content"
    "footer footer footer";

  /* Spacing */
  gap: 20px;
  row-gap: 20px;
  column-gap: 20px;

  /* Auto placement */
  grid-auto-rows: 120px;
  grid-auto-columns: 100px;
  grid-auto-flow: row;

  /* Alignment inside each cell */
  justify-items: center;
  align-items: center;

  /* Shorthand for above */
  place-items: center;

  /* Align entire grid inside container */
  justify-content: center;
  align-content: center;

  /* Shorthand */
  place-content: center;

  height: 100vh;
}
```
### Properties of Item class
```css
.item {
  /* Manual placement */
  grid-column: 1 / 3;
  grid-row: 2 / 4;

  /* Individual start/end */
  grid-column-start: 1;
  grid-column-end: 3;

  grid-row-start: 2;
  grid-row-end: 4;

  /* Named area */
  grid-area: content;

  /* Self alignment */
  justify-self: center;
  align-self: center;

  /* Shorthand */
  place-self: center;
}
```
