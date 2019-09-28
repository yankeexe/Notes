# Vue Notes

**General things to know:**

- Declarative Binding, one of the fundamental topics in vuejs. It binds the ui with the business logic. It also triggers reactive updates on the state of an application
- TSS -> Template, Script, Style
- Vue does not render html, it just renders text.
- We can write JS code in any Vue instances as long as it is a single expression and doesn't contains loops. Vue instances = places where we use {{ }} and directives with v- keyword.
- v-on can be replaced with `@` sign, and the v-bind can be replaced with `:attribute`.
- Do not use arrow function `=>` with lifecylce hook like `created`, `update`, `mounted`, and such. Also don't use them along with Vue property instances like `$el`, and `$data`

**Example:**

```html
<div id="app">
  <button v-on:click="counter++">Increase</button>
  <button @click="counter--">Decrease</button>
  <p>{{ counter }}</p>
  <a v-bind:href="link">GitHub</a>
  <a :href="link2">Reddit </a>
</div>

<script>
  new Vue({
    el: "#app",
    data: {
      counter: 0,
      link: "https://www.github.com",
      link2: "https://www.reddit.com"
    }
  });
</script>
```

### Computed Properties

Computed properties only triggers changes when it needs to on the ui. Else it sits idle. It caches the result. Vue "methods" run after every event, but computed will calculate the value internally.

Computed is used for carrying out heavy operations, the result of the operation is cached until its reactive dependencies changes. In case of `methods` it runs everytime when the UI re-renders and it can be an expensive task when we carry heavy operations with methods.

These properties are `getter` by default. We can provide setter when we need them. [Computed Setters](https://vuejs.org/v2/guide/computed.html#Computed-Setter)

[Read more](https://flaviocopes.com/vue-computed-properties/)

### Watchers

Watcher is used when we have to perform some asynchronous task like calling an API. [Read more](https://vuejs.org/v2/guide/computed.html#Watchers)

## Modifiers

Modifiers are keywords that are used after the directives with the .syntax. Normal modifiers are used to stop, prevent and other stuffs. Key modifiers are used to specify the key that is being pressed and is usually used with the keyboard events.

Modifiers can be chained with the dot syntax. `v-on:keyup.enter.space`

**Example: Key Modifiers**

Here the key modifier will make sure that the function is called, only when the enter key is pressed. For other keys we can write the key code. There are default key modifiers, [read here.](https://vuejs.org/v2/guide/events.html#Key-Modifiers)

```html
<div id="app">
  <input type="text" v-on:keyup.enter="alertMe" />
</div>

<script>
  new Vue({
    el: "#app",
    methods: {
      alertMe: function() {
        alert("Hey Alert");
      }
    }
  });
</script>
```

### Passing custom arguments and events

If we want to pass an argument when handling an event we can do so by writing the paramteres inside of the function call. If we want to send out both the parameter and the event object to our function then we can do so with the `$event` keyword. This is just in case, if we need both.

**Example:**

```html
<div id="app">
  <button v-on:click="incrementCounter(2, $event)">Increment</button>
  <p>{{ counter }}</p>
</div>

<script>
  new Vue({
    el: "#app",
    data: {
      counter: 0
    },
    methods: {
      incrementCounter: function(step, $event) {
        this.counter += step;
      }
    }
  });
</script>
```

## Directives in VueJS

### Two way data binding using v-model

Two way data binding means:

1. When properties in the model get updated, so does the UI.
2. When UI elements get updated, the changes get propagated back to the model.

We can achieve two-way data binding in Vue using the v-model directive. It can be used in input and form tags only ([read more](https://vuejs.org/v2/api/#v-model)). With this, change in one place is reflected everywhere on the UI wherever Vue instance is being used.

**Example with v-model:**
This makes binding code shorter and workflow more easier.

```html
<div id="app">
  <input type="text" v-model="info" placeholder="Write some info" />
  <p>The title is {{ info }}</p>
  <p>This is {{ info }}</p>
  <p></p>
</div>

<script>
  new Vue({
    el: "#app",
    data: {
      info: ""
    }
  });
</script>
```

**Example with v-on:keyup:**

```html
<div id="app">
  <input type="text" v-on:keyup="updateInfo" placeholder="Write some info" />
  <p>The title is {{ info }}</p>
  <p>This is {{ info }}</p>
  <p></p>
</div>

<script>
  new Vue({
    el: "#app",
    data: {
      info: ""
    },
    methods: {
      updateInfo: function(e) {
        this.info = e.target.value;
      }
    }
  });
</script>
```

---

### Rednering complete html using v-html

Vue does not render HTML, it just renders text by default. To make VueJS render HTML we have to use the `v-html` directive along with the content we want to render. It is prone to XSS vulenrabilites, use it wisely.
**Example:**

```html
<div id="app">
  <p v-html="link"></p>
</div>

<script>
  new Vue({
    el: "#app",
    data: {
      link: '<a href="https://www.github.com" target="#">Github </a>'
    }
  });
</script>
```

---

### Making content static with v-once directive:

Whenever we want to keep a content on the page static and don't want it's value to be overwritten we use the v-once directive.

It can be used directly inside of an html tag. Even though, the title value is being changed with the `changeTitle()` function, the `v-once` maintains the initial value of the title.
**Example:**

```html
<div id="app">
  <h1 v-once>{{ title }}</h1>
  <p>{{ changetitle() }}</p>
</div>

<script>
  new Vue({
    el: "#app",
    data:{
      title: "Welcome to Vue"
    },
    methods{
      changeTitle: function(){
        return (this.title = "Hello Vue")
      }
    }
  })
</script>
```

---

### Handling link attribute with v-bind directive:

If we want to use the Vue syntax using curly braces inside of a HTML attribute, it will not work. To make it work, we can use the `v-bind` attribute along with the `href` attribute of the anchor tag `<a> </a>`

**Example: **

```html
<div id="app">
  <!--This will not work -->
  <a href="{{" link }}> Go Here </a>

  <!-- This will work. No curly braces required when the vue instance is in control.  -->
  <a v-bind:href="link"> GO There </a>
</div>

<script>
  new Vue({
    el: "#app",
    data: {
      link: "https://www.google.com"
    }
  });
</script>
```

---

## Conditionals and Lists

### Conditional rendering using v-if and v-else

With `v-if` we can either attach an element to the DOM or detach it along with the `span` elements it carries.

`v-else` is must **immediately** follow `v-if`. It is like the general else block for if statement. There's also `v-else-if`. [Read More](https://vuejs.org/v2/guide/conditional.html)

**Example:**

```html
<div id="app">
  <p v-if="show">Now I am visible</p>
  <p v-else>I am visible now.</p>
  <p>I am always visible.</p>
  <button v-on:click="show = !show">Toggle</button>
</div>

<script>
  new Vue({
    el: "#app",
    data: {
      show: true
    }
  });
</script>
```

---

### Group Conditional Rendering using 'template'

`<template>` can be used to nest multiple elements which can be rendered conditionally.

**Example:**

```html
<div id="app">
  <p>You can see me always</p>
  <template v-if="show">
    <p>You can't</p>
    <h3>See</h3>
    <p>me</p>
  </template>
  <button v-on:click = "show != show"> Toggle </button>
</div>

  <script>
    new Vue({
      el: "#app",
      data: {
        show: true
      }
    });
  </script>
</div>
```

---

### Conditional Rendering using v-show

`v-if` completely attaches or detaches an element from the DOM. But if we just want to hide the element we can use the `v-show` directive.

This directive just adds the `display: none` property to that element hiding it from the view. We can check this with inspect element.

**Example:**

```html
<div>
  <p>Hello there</p>
  <p v-show="show">I come and go.</p>
  <button v-on:click="show != show">Toggle</button>
</div>

<script>
  new Vue({
    el: "#app",
    data: {
      show: true
    }
  });
</script>
```

---

### Rendering list with v-for

Like the regular `for` loop we can use the `v-for` directive to loop through a list of data and render the element.

Whenever we are using `v-for` it is recommended to use `key` attribute. In simple list rendering it may not be necessary but for a complex rendering it is required. Keys has to be binded with usually the id of the individual list item. `<li v-for = "item in bag" v-bind:key="item.id"></li>`

**Example:**

```html
<div id="app">
  <ul>
    <li v-for="item in ingredients" v-bind:key="item.id">{{item}}</li>
  </ul>
</div>

<script>
  new Vue({
    el: "#app",
    data: {
      ingredients: ["onion", "garlic"]
    }
  });
</script>
```

---

We can also pass a second argument in the `v-for` directive **inside of a parenthesis**, it is the index of the items in the list. [Read more](https://vuejs.org/v2/guide/list.html#Mapping-an-Array-to-Elements-with-v-for)

**Example:**

```html
<div>
  <ul>
    <li v-for="(item,i) in ingredients">{{item}} - {{i}}</li>
  </ul>
</div>

<script>
  new Vue({
    el: "#app",
    data: {
      ingredients: ["onion", "garlic", "pepper"]
    }
  });
</script>
```

---

### Rendering item in loop for various elements using 'template'

With the`v-for` on every element, we are able to render elements inside of that item only. To expand the placement of items in an array to different elements we can put the items inside of the `<template>` element.

**Example:**

```html
<div id="app">
  <template v-for="(item, i) in ingredients">
    <h1>{{item}}</h1>
    <p>{{i}}</p>
  </template>
</div>

<script>
  new Vue({
    el: "#app",
    data: {
      ingredients: ["onion", "garlic", "pepper"]
    }
  });
</script>
```

---

## Components

---


### General Notes:

- Components support all the options like data, computed, methods, watch and such except few root specific options like `el`.
- When we use data in component, data has to be a function that returns an object so that each instance of the component has different return values.

