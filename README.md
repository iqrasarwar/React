# React
#### What is React?
React is a declarative, efficient, and flexible, free and open-source front-end JavaScript library for building user interfaces based on UI components. It lets you compose complex UIs from small and isolated pieces of code called “components”. It is maintained by Meta and a community of individual developers and companies.<br />
> Imperative code instructs JavaScript on how it should perform each step. With declarative code, we tell JavaScript what we want to be done, and let JavaScript take care of performing the steps.

#### What are the major features of React?
- JavaScript XML or JSX (JavaScript Syntax Extension)
- Virtual DOM
- One-way data binding
- React Native
- Declarative UI
- Component Based Architecture
- Conditional statements

#### What is the difference between Element and Component?
**React Element**: It is the basic building block in a react application, it is an object representation of a virtual DOM node. React Element contains both type and property. It may contain other Elements in its props. React Element does not have any methods, making it light and faster to render than components.
You can create elements using following ways.
- JSX  `const element =<h1></h1>;`
- React.createElement( ) It will take up three parameters:- type of the element, properties, and children for creating an element.
`const element = React.createElement(
                  'h1',
                  {id:'header'},
                  'Hello world' );`

**React Component**: It is independent and reusable. It returns the virtual DOM of the element. One may or may not pass any parameter while creating a component. A component can be further described into functional components and class components.
```
function Hello(user){
   return <div>Hello {user.name} </div>
}
const element = <Hello name="John"/>
```
#### What is JSX?
JSX is a JavaScript Extension Syntax used in React to easily write HTML and JavaScript together. JSX produces React “elements”. React doesn’t require using JSX, but it is helpful as a visual aid when working with UI inside the JavaScript code. It also allows React to show more useful error and warning messages.
- You can put any valid JavaScript expression inside the curly braces in JSX.
```
const name = 'John';
const element = <h1>Hello, {name}</h1>;
const ele = <h1>{2+2}</h1>;
```
- You can use JSX inside of if statements and for loops, assign it to variables, accept it as arguments, and return it from functions.
- You may use quotes to specify string literals as attributes:
```
const element = <a href="https://www.reactjs.org"> link </a>;
```
- You may also use curly braces to embed a JavaScript expression in an attribute:
```
const element = <img src={user.avatarUrl}></img>;
```
- If a tag is empty, you may close it immediately with />, like XML:
```
const element = <img src={user.name} />;
```
- JSX tags may contain children:
```
const element = (
  <div>
    <h1>Hello!</h1>
  </div>
);
```
- You can never inject anything that’s not explicitly written in your application. Everything is converted to a string before being rendered. This helps prevent XSS (cross-site-scripting) attacks.

#### How to create components in React?
There are two ways to define components in ReactJS.
- **React functional components** can be any JavaScript function that returns the HTML. These functional components can also accept “props”, meaning properties or data. As these are JavaScript functions or extensions of JavaScript functions, they can also be created from the ES6 convention of the arrow function.There should only be one return per component.
```
const Hello = (props) => {
    const person = props.name;
  return (
    <div>
      <h1>Hello {person}!!</h1>
    </div>
  )
}
```
- The **class-based components** also have almost the same features as React function components. but before we define our class-based component, we need to import the “React. Component” or extract the Component like “{Component}” from React.
```
import React, { Component } from 'react'

class App extends Component {
  render() {
    return (
      <div>
        <h1>Hello {this.props.name}</h1>
      </div>
    )
  }
}
```
#### When to use a Class Component over a Function Component?
React Functional components were supposed to be stateless components having no support for life cycle methods.
But with the introduction of React hooks functional components can provide state managment via useState, useReducer hooks. They support lifecycle methods via the useEffect, useLayoutEffect hooks, and memoization via the memo HOC. Functional components are encouraged to used by meta & React. For furture info refer to :
[Class vs Functional Components](https://stackoverflow.com/questions/36097965/when-to-use-es6-class-based-react-components-vs-functional-es6-react-components)

#### What are Pure Components?

##### What is state in React?

##### What are props in React?

##### What is the difference between state and props?

##### Why should we not update the state directly?

##### What is the purpose of callback function as an argument of setState()?

##### What is the difference between HTML and React event handling?

##### How to bind methods or event handlers in JSX callbacks?

##### How to pass a parameter to an event handler or callback?

##### What are synthetic events in React?

##### What are inline conditional expressions?

##### What is "key" prop and what is the benefit of using it in arrays of elements?

##### What is the use of refs?

##### How to create refs?

##### What are forward refs?

##### Which is preferred option with in callback refs and findDOMNode()?

##### Why are String Refs legacy?

##### What is Virtual DOM?

##### How Virtual DOM works?

##### What is the difference between Shadow DOM and Virtual DOM?

##### What is React Fiber?

##### What is the main goal of React Fiber?

##### What are controlled components?

##### What are uncontrolled components?

##### What is the difference between createElement and cloneElement?

##### What is Lifting State Up in React?

##### What are the different phases of component lifecycle?

##### What are the lifecycle methods of React?

##### What are Higher-Order components?

##### How to create props proxy for HOC component?

##### What is context?

##### What is children prop?

##### How to write comments in React?

##### What is the purpose of using super constructor with props argument?

##### What is reconciliation?

##### How to set state with a dynamic key name?

##### What would be the common mistake of function being called every time the component renders?

##### Is lazy function supports named exports?

##### Why React uses className over class attribute?

##### What are fragments?

# Refrences
** https://reactjs.org/tutorial/tutorial.html
** https://stackoverflow.com/
** https://www.geeksforgeeks.org/

