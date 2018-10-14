# Notes I took while learning React JS. 

## Table of Contents: 
1. [Basic Introduction](#basic-introduction)

###  Basic Introduction

**Component:** Component is a Javascript function that returns HTML. We can also call the Components as View as they render elements in the display. 

**JSX:**
- JSX cannot be interpreted by the browser. 
- The purpose of JSX is that it gets inserted inside the DOM when we render the component containing JSX. JSX gets converted into HTML. 
- Basically, JSX is a Javascript code that produces HTML. JSX gets transpiled to vanilla JS using Babel. 
- JSX makes our much more cleaner, because writing the same code in plain JS would be a pain.
- wherever we use JSX we need to import the React package. 
- for multi-line JSX, we need to use () paranthesis after return keyword. 
 ---

**Rendering to the Dom:** 
- To render component to the DOM we need to pass the instance of the component to the ReactDOM.render(). Instance is <App />. 
Example:
```react 
ReactDOM.render(<App />, document.querySelector('.container'));
instead of: 
ReactDOM.render(App,document.querySelector('.container'));
```
---

**Class Components:**
- extending React.Component means providing our class with all the functionality that React.Component class has. 
- it must have a render method. 
- whenever we have a render function, we must **return** some JSX else it will throw an error.
- **constructor** is called everytime a new instance of the class is called. For example: `<App />` 
- constructor does a lot of things inside the class, one of the thing is initialize the state. 
- when we define a method that is already defined in the parent class, we can call that parent method on the parent class by calling **super**. 
-  
---

**Import package and name it directly:**
```react
import React, {Component} from 'react';
```
Here we are importing Component class from react package and assigning the variable named Component to it. 
It is same as writing: 
```react
const Component = React.Component; 
```

**State:**
- It is a plain javascript object used to record and react to user events. 
- Whenever a state is changed, the component re-renders along with its childrens. 
 

 
**Notes:** 
- Only one component per page, because React works better with isolation of functionality.
- put different components inside of /src/components folder for better organization. 
- don't forget to use "--save" flag whenever you are installing a new package to your project. 
- all of the JS files in react is silent to each other unless we explicitly define any connection between them.
- Only use class component whenever you want to save some data else functional component is fine. 
- small case in DOM name = HTML element, capital case in DOM name = JSX element.
Example: <div> is a HTML element. <App /> is a JSX element. 
- comment inside JSX: {/* Comment Goes Here! */}

## Redux
**Notes**
- Whenever we are thinking of saving data or making API request inside of a redux application, we have to do it through **ActionCreators**
- 

### ReduxForm
- Whenever we render the form, we have to export the form using reduxForm, where we give the form a uinque name. If we have some validation function, we mention it there as well with key value pair. Then on the second parenthesis, we pass the Container inside which our form is getting rendered.

    ![alt text](images/export_redux_form.png)

- ReduxForm handles just the state and validation of our form.
- There are three states in ReduxForm: pristine, touched and invalid. 
    - prisitne: it has not been selected, it has no user input 
    - touched: user has focused and focused out of the input
    - invalid: show error message 
- ```react
    {field.meta.touched ? field.meta.error : ''}
    ```



