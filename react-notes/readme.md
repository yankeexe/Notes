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
### Importing Stuffs
- **Import package and name it directly:**
    ```react
    import React, {Component} from 'react';
    ```
Here we are importing Component class from react package and assigning the variable named Component to it. 
It is same as writing: 
    ```react
    const Component = React.Component; 
    ```
- When we just want to render something on the display, we don't need the whole ReactDOM library, we can just import the render functionality from it. 
  ```jsx 
    import { render } from 'react-dom';

    render(< Component/>, TargeNode)
  ```
**State:**
- It is a plain javascript object used to record and react to user events. 
- Whenever a state is changed, the component re-renders along with its childrens. 
 
## Comments
---

comment inside JSX: `{/* Comment Goes Here! */}`
    - These comments are written usually inside the `return` statement, anywhere else we can use regular comments with `//`
    - Don't put the comment on the very first line of the return statement as it will throw an error. Use it after a sentence. 
    - Example: 
  
**Wrong Way**
```jsx
return(
    {/* This causes an error */}
    <p> This will not get rendered and cause an error </p>
);
```

**Right Way**
```jsx
return(
    <p>This will get rendered</p>
    {/* Comment here is fine */}
)
```
 ---
 ## `this` Binding 
 - `this` refers to the parent class in general. 
 - when we are writing `this` inside of the `render()` method, we are refering to the class in which it is called. 
 - when we have other helper function inside of the class, then the `this` mentioned inside the helper function is refering to the function itself. To make it refer to the parent class, we need to `bind` it to the parent class. 

**example:**

### **First Way** *(Efficient)*
```jsx
    class Person extends Component {
        constructor(props){
            super(props)
            this.state = {data: ''}
            /*Step 3: Bind the sendData `this` to the parent class. */
            this.sendData = this.sendData.bind(this);
        }
        sendData(){
            /*Step 2: Here `this` refers to the function sendData, to make it refer to the parent class we have to bind the function with the parent class */
            console.log(this.state.data)
        }
        render() {
            return (
                <form onSubmit = {this.sendData}>
                {/* Step 1: Here this, refers to the class Person, it takes sendData method of class function, it's like Person.sendData */}
                    <input value = {this.state.data} onChange={e => this.setState({data: e.target.value})} />
                    <button type="submit">Send Data</button>
                </form>
            );
        }
    }
```
### **Second Way**
```jsx
    class Person extends Component {
        sendData(){
            /*Step 2: Now the `this` mentioned here refers to the parent class Person. */
            console.log(this.state.data)
        }
        render() {
            return (
                <form onSubmit = {this.sendData.bind(this)}>
                {/* Step 1: Here the first `this` refers to the class Person, it takes sendData method of class function, it's like Person.sendData,
                then it binds the `this` of sendData() method to the parent class. */}
                    <input value = {this.state.data} onChange={e => this.setState({data: e.target.value})} />
                    <button type="submit">Send Data</button>
                </form>
            );
        }
    }
```

### **Third Way**
```jsx
    class Person extends Component {
        sendData(){
            /*Step 2: Now the `this` mentioned here refers to the parent class Person. */
            console.log(this.state.data)
        }
        render() {
            return (
                <form onSubmit = {e=> this.sendData(e)}>
                {/* Step 1: This method is inefficient because, it create a new function everytime it something has to refer to this helper*/}
                    <input value = {this.state.data} onChange={e => this.setState({data: e.target.value})} />
                    <button type="submit">Send Data</button>
                </form>
            );
        }
    }
```
 ---

 ## Refs
 Refs provide a way to access DOM nodes or React elements created in the render method.

**When to Use Refs**

There are a few good use cases for refs:

- Managing focus, text selection, or media playback.
- Triggering imperative animations.
- Integrating with third-party DOM libraries.
- Avoid using refs for anything that can be done declaratively.

> **Example:**

 Instead of using event to access value of the form we can use refs.

### **First way - Using String**
```jsx
        class Person extends Component {
        constructor(props){
            super(props)
            this.state = {data: ''}
            this.sendData = this.sendData.bind(this);
            this.getData = this.getData.bind(this);
        }
        sendData(){
            console.log(this.state.data)
        }
        getData(){
            this.setState({data: this.refs.evalue.value}) {/*Access the value of the DOM with the help of refs*/}
        }
        render() {
            return (
                <form onSubmit = {this.sendData}>
                    <input value = {this.state.data} onChange={this.getData} refs="evalue" /> {/*Expose the DOM using ref*/}
                    <button type="submit">Send Data</button>
                </form>
            );
        }
    }
```  

### **Second way -  Using Callback Function**
```jsx
        class Person extends Component {
        constructor(props){
            super(props)
            this.state = {data: ''}
            this.sendData = this.sendData.bind(this);
            this.getData = this.getData.bind(this);
        }
        sendData(){
            console.log(this.state.data)
        }
        getData(){
            this.setState({data: this.a.value}) {/*Access the value of the DOM with the help of refs, No need to mention refs*/}
        }
        render() {
            return (
                <form onSubmit = {this.sendData}>
                    <input value = {this.state.data} onChange={this.getData} refs={eval => this.a = eval} /> {/*Expose the DOM using ref*/}
                    <button type="submit">Send Data</button>
                </form>
            );
        }
    }
```  


 ---
**Notes:** 
- Only one component per page, because React works better with isolation of functionality.
- put different components inside of /src/components folder for better organization. 
- don't forget to use `"--save"` flag whenever you are installing a new package to your project. 
- all of the JS files in react is silent to each other unless we explicitly define any connection between them.
- Only use class component whenever you want to save some data else functional component is fine. 
- small case in DOM name = HTML element, capital case in DOM name = JSX element.
Example: <div> is a HTML element. <App /> is a JSX element. 
- Instead of using `document.getElementById` use `document.querySelector(id or class)`
    select id using `#id_name`, select class using `.className`
- For emmet support in JSX use the following setting in VSCode: 
    ```json 
        "emmet.includeLanguages":{
            "javascript": "javascriptreact",
        }
    ```

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



