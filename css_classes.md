# **CSS Structural Classes**

- Structural classes control:
1. Layout
2. Position
3. Alignment
4. Spacing
5. Display behavior
- They DO NOT control colors or design.They control structure.

## **A. Container Classes**
- Used to wrap sections.
```css
.container {
  width: 90%;
  max-width: 1200px;
  margin: 0 auto;
}
```
- Centers content
- Controls max width
- Creates consistent layout
- Used in almost every website.

## **B. Row / Column Classes**
- Used for grid-like layouts.
```css
.row {
  display: flex;
}
.col {
  flex: 1;
}

traditional:
.row {
  display: flex;
  gap: 20px;
}
```
## **C. Flex Utility Classes**
```css
.flex {
  display: flex;
}
.flex-center {
  display: flex;
  justify-content: center;
  align-items: center;
}
.flex-between {
  display: flex;
  justify-content: space-between;
}
.flex-column {
  display: flex;
  flex-direction: column;
}
```
- Used everywhere in real-world projects.

## **D. Positioning Classes**
```css
.relative {
  position: relative;
}
.absolute {
  position: absolute;
}
.fixed {
  position: fixed;
}
```
- These are structural because they affect layout flow.

## **E. Display Classes**
```css
.block {
  display: block;
}
.inline {
  display: inline;
}
.inline-block {
  display: inline-block;
}
.hidden {
  display: none;
}
```
## **F. Width & Height Helpers**
```css
.w-100 {
  width: 100%;
}

.h-100 {
  height: 100%;
}

.full-screen {
  height: 100vh;
}
```
## **G. Overflow Control**
```css
.overflow-hidden {
  overflow: hidden;
}
.scroll-y {
  overflow-y: auto;
}
```
## **H. Z-index Helpers**
```css
.z-1 { z-index: 1; }
.z-10 { z-index: 10; }
.z-100 { z-index: 100; }
```


# **CSS Styling Classes**
- Styling classes control:
1. Colors
2. Fonts
3. Borders
4. Background
5. Visual appearance
- They DO NOT affect layout structure.

## **A. Background Classes**
```css
.bg-primary {
  background-color: blue;
  background-color: #333;
  background-color: #f5f5f5;
}
```
## **B. Text Styling Classes**
```css
.text-center {
  text-align: center;
  font-weight: bold;
  font-size: 12px;
  color: blue;
}
```
## **C. Border Classes**
```css
.border {
  border: 1px solid #ccc;
  border-radius: 8px;
  border-radius: 50%;
}
```
## **D. Shadow Classes**
```css
.shadow {
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  box-shadow: 0 8px 20px rgba(0,0,0,0.2);
}
```
## **E. Spacing Utility Classes**
Instead of writing custom margin everywhere:
```css
.mt-10 { 
    margin-top: 10px; 
    margin-bottom: 20px;  
    padding: 10px; 
    padding-left: 20px; padding-right: 20px; 
}
```
### Real Example (Clean Architecture)
```html
<div class="container">
  <div class="card shadow p-20">
    <h2 class="text-center text-bold">Title</h2>
  </div>
</div>
```
- container → structure
- card → structure
- shadow → styling
- p-20 → spacing utility
- text-center → styling
- text-bold → styling
