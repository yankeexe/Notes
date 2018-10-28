# Note for CSS

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

**Root Selector**
- `html` is the root selector. 
  Example: 
  ```css 
    html {
        font-size:10px;
    }
  ```
---
**Box Sizing**
- Whenever we define the height and width of boxes in the webpage, their actual height and width will be the sum of padding and border (if any).
Example: 

| Property | Actual value |
| --- | ----------- |
| height | height + border + padding |
| width | width + border + padding | 

- This will always result in boxes that are larger in size than the defined value. To overcome this, we use `box-sizing`. 
- The `box-sizing` property allows us to include the padding and border in an element's total width and height.
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
- **CSS Value Processing**

    <img src="https://i.imgur.com/LDNOmQw.png" width="550" height="250">
- **CSS Inheritance**
  
  <img src="https://i.imgur.com/KAgZLtu.png" width="550" height="250">
---
## CSS Layout
- To define the absolute position of an element, we first have to set the property of its parent element to relative i.e `position: relative;`. And in accordance with the parent property, we can set the exact position of the item with `position: absolute;` property. 
---
## CSS Specifity
- This is bascially choosing which selector to choose if there are same property mentioned with different selectors. 
- The hierarchy is like this: 
  
  <img src="https://webdevstudios.com/wp-content/uploads/2015/05/specificity1.png" width="350" height="150">
- A selector with 1 id is more specific than the selector with 1000 classes. `(0,1,1000,0)`
- A selector with 1 class is more specific than the selector with 1000 elements. `(0,0,1,1000)`
- The universal selector `*` has no specifity `(0,0,0,0)`. And any other selector can override it.
- The count increases by one if there are same types of selectors which will add up to its weight contributing in the decision making - which style to apply.
- We evaluate the priority from left to right.
- The winner of the value is called the cascaded value, which contributes to the name of **CSS (Cascading Style Sheet)**.
- What happens if two selectors have the same weight or specifity?
  >The last declaration in the code will override all other declarations and it will be applied.
- CSS declarations marked with `!important` have the highest priority - but use it as a last source. We should work based on specifity most often for cleaner and maintainable code.
- Rely more on specifity than the order of selectors.
- But rely on order when using 3rd party stylesheets - always put your own stylesheet last.

---
## CSS Animations
 **Transform Translate**
 - Putting the value of translate to zero will bring it back to the orginal form. 
 - Just think of it as X and Y axis, the beginning position `(0,0)` and then you start from there.
 - Animation is specified using the `@keyframes` keyword followed by the name of the animation where the syntax is 
  ```css
  @keyframe anmiation-name {
      animation timeline (can be 0, 10, 20 upto 100){

      }
      animation timeline2 (can be any time apart from the one mentioned above upto 100){

      }
  }
  ```
 - To use the aniamtion in any of our elements, we just have to set the animation name with the animation name propety. Example: 
  ```css 
    .className {
        animation-name: nameOfTheAnimation; 
        animation-duration: specify time in terms of seconds or milliseconds;
        animation-delay: how long to wait before the animation starts - measured in s and ms;
        animation-iteration-count: specify how many times to play the animation; 
    }
  ```
 - We can use all of these properties inside of a single property called `animation`. We have to separate each of the value with space and no commas. CSS will figure out itself what is what.
 - It will take property in this order: `animation-name, animation-duration, animation-timing-function, animation-delay, animation-iteration-count, animation-direction, animation-fill-mode, and animation-play-state`.
  ```css 
    .className {
        animation: nameOfTheAnimation duration timing function
    }
  ```
  **Backface Visibility**
  - Whenever we are transforming an element, suppose rotating an element 180 degrees we can see the background of that element, to eliminate that, we use the `backface-visibility` property as `hidden` to not show it. 
  - It can also be used to fix shakiness in the animation.
  ```css
    .className {
        backface-visibility: hidden;
    }
  ```
  **Animation Fill Mode**
  - It is used to apply the animation to an element before the page loads when it is set to backwards by retaining the `animation-delay` property.
  Example: 
  ```css
    .className {
        animation-fill-mode: backwards;
    }
  ```
  **Pseudo Elements and Pseudo Classes**
    - 

 > [Reference Translate](https://cssreference.io/property/transform/)

 > [Animation Timing Function Ref](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-timing-function)

---


**Basic Notes**
- If you want to use font universal to the page, use it inside of the `body`. 
- Change `line-height` based on the `font-size`
- `display: block;` makes the element occupy the whole width of the display.
- To fade something out put the `opacity: 0;`
---

**To Learn**
- [ ] Units in CSS 

---

**Learning Resources**
- [Learn CSS Layout](http://learnlayout.com/)
- [CSS Reference](https://cssreference.io)
- [CSS MDN](https://developer.mozilla.org/en-US/docs/Web/CSS)