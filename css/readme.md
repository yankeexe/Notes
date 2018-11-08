

# Notes on CSS - SCSS :nail_care:

**Table of Contents**
- [Notes on CSS - SCSS](#notes-on-css---scss)
- [CSS (Cascading Style Sheets)](#css-cascading-style-sheets)
    - [Units in CSS](#units-in-css)
    - [CSS Layout](#css-layout)
    - [CSS Typography](#css-typography)
    - [CSS Specifity](#css-specifity)
    - [CSS Animations](#css-animations)
- [SCSS (Sassy CSS)](#scss-sassy-css)
    - [Nesting in SCSS](#nesting-in-scss)
    - [Clearfix Hack](#clearfix-hack)
    - [Mixins](#mixins)
    - [Functions](#functions)
    - [Extends](#extends)
# CSS (Cascading Style Sheets)

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

**Box Types**


<img src="https://i.imgur.com/fyh3jfl.png" height="350" width="650">

**Position Scheme**

<img src="https://i.imgur.com/wjYiBKz.png" height="350" width="650">
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

## CSS Typography

**text-transform**

- ###### To change the text to uppercase, lowercase, and so on use `text-transform
---

## Basic Responsive Design Principles

<img src="https://i.imgur.com/O6evbZH.png" width="550" height="250">

---

## CSS Layout
### CSS Layout Types

**Float Layouts**

- Placing boxes side by side using `float`

**Flexbox**

- Arrange items in one dimensional row
- It is a content first approach.

**CSS Grid**

- Used for 2 dimensional layout of the page. 
- It is a layout first approach.

### width vs. max-width

**width:**  

- a block-level element always takes up the full width available 
  (stretches out to the left and right as far as it can).
- Setting the `width` of a block-level element will prevent it from stretching 
  out to the edges of its container. Then, you can set the 
  margins to auto, to horizontally center the element within its container. The 
  element will take up the specified width, and the remaining space will be split 
  equally between the two margins.

**max-width:**

- The `max-width` property defines the maximum width of an element.
- If the content is larger than the maximum width, it will automatically change 
  the height of the element.
- If the content is smaller than the maximum width, the `
  max-width` property 
  has no effect.
- This prevents the value of the `width` property from becoming larger than `max-width`



> **Reference:** [width vs max-width](https://css-tricks.com/tale-width-max-width/)

### Center Block Elements

**Center Block Element inside of another block element:** 

- `margin: 0 auto;`

  Here the first value `0` represents the top and bottom margin value, while the second value `auto` represents the left and right margin value.

- setting to `auto` means, the browser when loading the page will try to put margin  on both left and right,  and since both are set to auto, the item is centered.

### :not pseudo class elements

- ` :not(selector)` is used to apply changes to all the elements except the defined element. 
- usually the defined element is determined using the `last-child` and similar pseudo selectors.
- Suppose we want to apply `margin-bottom` of `90px` on all of our rows but we don't want that margin on the last row. So what we can do is select the last row using `:last-child` selector with `:not` class.
- This will select every other child and apply the effect.

**Example: 1 **

```scss
.row {
     max-width: $grid-width;
    background-color: #eee;
    margin: 0 auto;
   
    &:not(:last-child) { //everything except the last child.
    	margin-bottom: 90px;
    }
}
```



**Example: 2** 

  ```scss
    :not(p) {
        background: #eee; //apply background color to everything except the paragraph tag.
    }
  ```

### calc() function 

- Perform mathematical operations.

- Mixing units is one of the most important feature of the calc() function. If one unit is in  rem, another can be in percentage and so on.

- If we want to use the variable inside of the `calc()` function then we have to wrap it with `#{}`

  **Example:**`#{$gutter-horizontal}`

### Attribute Selector []

- An element can have attributes like `alt` `src` `class` `ahref` `target` and so on. If we want to style elements with similar attributes, then we use the attribute selector. 

- ^ = starts with 

- $ = ending with

- *=select all

  **Example:**

  Select all the classes that starts with `col-` and apply style to them.

  ```scss
  [class^="col-"] {
      background-color: orangered;
      float: left;
  
      &:not(:last-child) {
          margin-right: $gutter-horizontal;
      } 
  }
  ```

  ### General Notes on CSS Layout

- To define the absolute position of an element, we first have to set the property of its parent element to relative i.e `position: relative;`. And in accordance with the parent property, we can set the exact position of the item with `position: absolute;` property. 

---

## CSS Specificity

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
 - Putting the value of translate to zero will bring it back to the original form. 
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

 > [Reference Translate](https://cssreference.io/property/transform/)

 > [Animation Timing Function Ref](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-timing-function)

---


**Basic Notes**
- If you want to use font universal to the page, use it inside of the `body`. 
- Change `line-height` based on the `font-size`
- `display: block;` makes the element occupy the whole width of the display.
- To fade something out put the `opacity: 0;`
- Comment on CSS files is: `/* Comment */`
- 
---

**To Learn**
- [ ] Units in CSS 
- [ ] What is z-index

---

**Learning Resources for CSS**
- [Learn CSS Layout](http://learnlayout.com/)
- [CSS Reference](https://cssreference.io)
- [CSS MDN](https://developer.mozilla.org/en-US/docs/Web/CSS)
- [Block Element Modifier - Naming Convention](http://getbem.com/introduction/)
- [Atomic Design Methodology](http://atomicdesign.bradfrost.com/chapter-2/)

# SCSS (Sassy CSS)
<img src= "https://i.imgur.com/gOfK2Ko.png" height="350" width="650">

- SASS and SCSS are almost the same thing, SCSS is the extension of SASS which is quite similar to CSS. 
- SASS uses indentation without curly braces or semi-colons which can be difficult so we use SCSS, which has all the feature of SASS but it is syntatically a bit different.
- Valid **CSS** is a valid **SCSS**

## Nesting in SCSS
- In normal CSS we have create different selector for parent and the children.
**Example: Normal CSS**
```html
<nav>
    <ul class="navigation">
        <li>About us</li>
        <li> Contact Us </li>
        <li> Request a quote</li>
    </ul>
</nav>
```
```css
    .navigation {
        list-style: none;
    }
    .navigation li {
        display: inline-block;
        margin-left: 30px;
    }

    .navigation li:first-child {
        margin: 0;
    }
```
> Resource: [CodePen Nesting](https://codepen.io/yankexe/pen/oaOvEL?editors=1100)
---
**Example: SCSS**
- In SCSS we can created a nested block inside of the parent selector.
- `&` represents the path till the nested element. In the example below, the `&` represents the path: 
    - `.navigation li:first-child` which is the second level nest.
- `&` is basically used when pseudo classes are involved. 

```scss
    .navigation { //parent selector
        list-style: none; 

        li { //first level nest
            display: inline-block;
            margin-left: 30px;

            &:first-child { //second level nest
                margin: 0;
            }
        }
    }
```
## Clearfix Hack
- Elements after a floating element will flow around it.  
- Usually used when we use the `float` property.

<img src="https://i.imgur.com/OhoR4sA.png" height="250" width="950">


```css
.clearfix::after {
    content: "";
    clear: both;
    display: table;
}
```

## Mixins
- Mixins are here for the purpose of code reusability. DRY(Don't Repeat Yourself)
- They are like variables that hold a chunk of code. 
- Use `@mixin` keyword to declare a mixin. 
- Use `@include` keyword to add mixin property to the selector. 

**Syntax:**
```scss
//Declaring mixins
    @mixins variableName {
        property
    }

//using mixins 
 nav {
     @include variableName;
 }
```
- Mixins can also take parameters which will help to define different property on some styles. 

```scss
    //declaring mixin with params
    @mixin style-link-text($color) {
        text-decoration: none;
        text-transform: uppercase;
        color: $color; 
    }

    //using mixins with params
    @include style-link-text(red);
```
- When params are defined, each instance of the mixn must pass the value as an argument else it is going to throw an error.

## Functions 
- Functions are like JS functions which takes arguments, performs actions and return a value.

  **Syntax:**

  ```scss
    @function functionName ($a, $b) {
        @return //action
    }  
  ```
  **Example:**
    ```scss
    //declare a function
        @function divide ($a, $b) {
            @return $a / $b;
        }
  
        //use function
        nav {
            margin: divide(300,10) * 1px;
        }
  
    ```

- `*1px` is a workaround because, when a value is returned by the `divide` function, it has no units at all which CSS cannot process. To give it a unit, we multiply it by `*1unit`

## Extends 
- Extends are kind of like Mixins, they are palceholder for styles. 
- The difference between Mixin and Extends is that, Mixin replaces the mixin variable with the code whereas in extend, it changes the variable name of the selector above the code block with the selector it is defined inside.
- Use extends only if the elements/selectors are related, else stick with mixins.

**Example**
```scss 
    //Extend Definition 
    %btn-placeholder { //------> %btn-placeholder will get replaced by btn:link
        padding: 10px;
        display: inline-block;
        text-align: center;
    }

    //Use Extend 
     btn:link {
         @extend %btn-placeholder
     }
```

**Notes**
- Sass is always written like this, no uppercase for all the letters, while SCSS is written in total capital.
- Comment in SCSS is same as of JS. `//Comment here!` 

**To Learn**
- [ ] 

**Learning Resources for SASS**
- [SASS Official Docs](https://sass-lang.com/guide)


