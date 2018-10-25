# Note for CSS and its frameworks. 

**Universal Selector**
- If we want to apply css to all the elements of the webpage, then we use the universal selector. 
  Example: 
  ```css 
    * {
        margin: 0;
        padding: 0;
    }
  ```
- `*` is the universal selector
---
**Box Sizing**
- Whenever we define the height and width of boxes in the webpage, their actual height and width will be the sum of padding and border. 
Example: 

| Property | Actual value |
| --- | ----------- |
| height | height + border + padding |
| width | width + border + padding | 

- This will always result in boxes that are larger in size than the defined value. To overcome this, we use `box-sizing`. 
- The box-sizing property allows us to include the padding and border in an element's total width and height.
If you set `box-sizing: border-box;` on an element padding and border are included in the width and height.

> [Reference Box Sizing](https://www.w3schools.com/css/css3_box-sizing.asp)
---
**Clip Path**
- The clip-path property in CSS allows you to specify a specific region of an element to display, rather than showing the complete area.
- There are 4 points we should consider, each with its x and y axis and determine how much of it we want to show. Based on that we can create different patterns. 
- syntax: 
```css
    img {
        clip-path: polygon(x y, x y,x y,x y);
    }
```
> [Make Clip-path Visual Tool](https://bennettfeely.com/clippy/)
---
## Units in CSS
**View Height (vh)**
- usually used in background image. 
- Determines how much of the current view of the height the image should cover. 
Example: 
```css
    body {
        height: 50vh; /*This will cover the 50% of the view of the current window  */
    }
```
---
## CSS Layout
- To define the absolute position of an element, we first have to set the property of its parent element to relative i.e `position: relative;`. And in accordance with the parent property, we can set the exact position of the item with `position: absolute;` property. 
---


**Basic Notes**
- If you want to use font universal to the page, use it inside of the `body`. 
- Change `line-height` based on the `font-size`
- `display: block;` makes the element occupy the whole width of the display.

---

**To Learn**
- [ ] Units in CSS 

---

**Learning Resources**
- [Learn CSS Layout](http://learnlayout.com/)
- [CSS Reference](https://cssreference.io)