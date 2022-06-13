# React

### What is React?

React is a declarative, efficient, and flexible, free and open-source front-end JavaScript library for building user interfaces based on UI components. It lets you compose complex UIs from small and isolated pieces of code called “components”. It is maintained by Meta and a community of individual developers and companies.<br />

> Imperative code instructs JavaScript on how it should perform each step. With declarative code, we tell JavaScript what we want to be done, and let JavaScript take care of performing the steps.

### What are the major features of React?

- JavaScript XML or JSX (JavaScript Syntax Extension)
- Virtual DOM
- One-way data binding
- React Native
- Declarative UI
- Component Based Architecture
- Conditional statements

### What is the difference between Element and Component?

**React Element**: It is the basic building block in a react application, it is an object representation of a virtual DOM node. React Element contains both type and property. It may contain other Elements in its props. React Element does not have any methods, making it light and faster to render than components.
You can create elements using following ways.

- JSX `const element =<h1></h1>;`
- React.createElement( ) It will take up three parameters:- type of the element, properties, and children for creating an element.
  `const element = React.createElement( 'h1', {id:'header'}, 'Hello world' );`

**React Component**: It is independent and reusable. It returns the virtual DOM of the element. One may or may not pass any parameter while creating a component. A component can be further described into functional components and class components.

```
function Hello(user){
   return <div>Hello {user.name} </div>
}
const element = <Hello name="John"/>
```

### What is JSX?

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

### How to create components in React?

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

### When to use a Class Component over a Function Component?

React Functional components were supposed to be stateless components having no support for life cycle methods.
But with the introduction of React hooks functional components can provide state managment via useState, useReducer hooks. They support lifecycle methods via the useEffect, useLayoutEffect hooks, and memoization via the memo HOC. Functional components are encouraged to used by meta & React.<br />
For furture info refer to : [Class vs Functional Components](https://stackoverflow.com/questions/36097965/when-to-use-es6-class-based-react-components-vs-functional-es6-react-components)

### What are Pure Components?

A React component is considered pure if it renders the same output for the same state and props. For this type of class component, React provides the PureComponent base class. Class components that extend the React. PureComponent class are treated as pure components.

```
class Pure extends React.PureComponent{
   render(){
      return <h1>This is Pure Component!</h1>;
   }
}
```

The difference between them is that React.Component doesn’t implement shouldComponentUpdate(), but React.PureComponent implements it with a shallow prop and state comparison. If your React component’s render() function renders the same result given the same props and state, you can use React.PureComponent for a performance boost in some cases.
A function is said to be pure if the return value is determined by its input values only and the return value is always the same for the same input values.There seem two ways to do it for React functional components:

Using **memo** from react:

```
import React, { memo } from 'react';
const Component = (props) {
  return (
    // Component code
  )
}
export default memo(Component);
```

Using **pure** from recompose:

```
import React from 'react';
import { pure } from 'recompose';
const Component = (props) {
  return (
    // Component code
  )
}
export default pure(Component);
```

### What is state in React?

The State of a component is an object that holds some information that may change over the lifetime of the component.The difference is while a “normal” variable “disappears” when their function exits, the state variables are preserved by React.

### What are props in React?

“Props” is a special keyword in React, which stands for properties and is being used for passing data from one component to another. The important part here is that data with props are being passed in a uni-directional flow. (one way from parent to child)
Furthermore, props data is read-only, which means that data coming from the parent should not be changed by child components.

```
function PropComponent({ name }) {
  return (<p>Your name {name}!</p>);
}
ReactDOM.render(
    <PropComponent name="john" />,
  document.getElementById("root")
);
```

### What is the difference between state and props?

The key difference between props and state is that state is internal and controlled by the component itself, it can be changed (Mutable).states are initialize on component mount.They are used for rendering dynamic changes within component.
while props are external and controlled by whatever renders the component.Props can't be changed.(Immutable).

### Why should we not update the state directly?

- Don't mutate this.state directly, as calling setState() afterwards may replace the mutation you made. Treat this.state as if it were immutable. setState() does not immediately mutate this.state but creates a pending state transition. Accessing this.state after calling this method can potentially return the existing value.
  setState() will always trigger a re-render unless conditional rendering logic is implemented in shouldComponentUpdate(). If mutable objects are being used and the logic cannot be implemented in shouldComponentUpdate(), calling setState() only when the new state differs from the previous state will avoid unnecessary re-renders.
- when we update the state of a component all it's children are going to be rendered as well. or our entire component tree rendered. But when i say our entire component tree is rendered that doesn’t mean that the entire DOM is updated. when a component is rendered we basically get a react element, so that is updating our virtual dom. React will then look at the virtual DOM, it also has a copy of the old virtual DOM, that is why we shouldn’t update the state directly, so we can have two different object references in memory, we have the old virtual DOM as well as the new virtual DOM.
  then react will figure out what is changed and based on that it will update the real DOM accordingly .

### What is the purpose of callback function as an argument of setState()?

setState works in an asynchronous way. That means after calling setState the this.state variable is not immediately changed. so if you want to perform an action immediately after setting state on a state variable and then return a result, a callback will be useful.

### What is the difference between HTML and React event handling?

**HTML**
we specify event using “onclick”,”onsubmit”which is the normal convention. We bind or provide the listener in form of the string. The string we pass to the listener should have “( )” at the end in order to work. We can add event listener any time using external javascript.
**React**
We specify the event using “onClick”,”onSubmit” likewise which is camel case convention.
We bind or provide the listener in form of function name or method name as a variable.
We are only suppose to pass the method name and nothing else. React can determine that it has to run this method.We have to specify all the Events at the time of creating the component.

### How to bind methods or event handlers in JSX callbacks?

- Binding in Constructor<br />

```
class Component extends React.Component {
  constructor(props) {
    super(props);
    this.handleClick = this.handleClick.bind(this);
  }
  handleClick() {
    // ...
  }
}
```

- Arrow functions in callbacks: Use Arrow Function binding whenever possible.

```
<button onClick={(event) => this.handleClick(event)}>{'Click me'}</button>
```

- Binding Event Handler in Render Method
  We can bind the handler when it is called in the render method using bind() method.

```
<button onClick={this.clickHandler.bind(this)}>Click</button>
```

Binding Event Handler using Arrow Function
We are binding the event handler implicitly. This approach is the best if you want to pass parameters to your event.

```
<button onClick={() => this.clickHandler()}>Click</button>
```

- Binding Event Handler using Arrow Function as a Class Property

```
clickHandler = () => {...}
...
<button onClick={this.clickHandler}>Click</button>
...
```

### How to pass a parameter to an event handler or callback?

If you want to pass a parameter to the click event handler you need to make use of the arrow function or bind the function. If you pass the argument directly the onClick function would be called automatically even before pressing the button.

```
...
 call(message,event) {
   alert(message);
 }
...
<button onClick={(event)=> this.call("Your message",event)}>Click the button!</button>
...
```

- we can use Bind Method that is also used to pass the parameters in functions of class-based components.

```
...
 call(message) { alert(message);}
...
<button onClick= {this.call.bind(this,"Your message")}>Click the button!</button>
```

### What are synthetic events in React?
With synthetic events, the same API interface is implemented across multiple browsers.
[synthetic events](https://blog.logrocket.com/getting-started-react-synthetic-event/)
### What are inline conditional expressions?
In the react, conditional rendering is the process to show components based on a particular condition.
- **Inline if-else conditional (ternary) operator**
```
<b>{total > 0 ?<h2>{total} left</h2> : <h2>Empty</h2> }</b>
```
- **Inline If with Logical && Operator**
```
{(total > 0) && <h2>{total} left</h2> }
```
### What is "key" prop and what is the benefit of using it in arrays of elements?
A key is a special string attribute you should include when creating arrays of elements. Key prop helps React identify which items have changed, are added, or are removed. Most often we use ID from our data as key:
```
const todoItems = todos.map((todo) => <li key={todo.id}>{todo.text}</li>);
```
When you don't have stable IDs for rendered items, you may use the item index as a key as a last resort:
```
const todoItems = todos.map((todo, index) => <li key={index}>{todo.text}</li>);
```
- Using indexes for keys is not recommended if the order of items may change. This can negatively impact performance and may cause issues with component state.
- If you extract list item as separate component then apply keys on list component instead of li tag.
- There will be a warning message in the console if the key prop is not present on list items.
### What is the use of refs?
There are a few good use cases for refs:
- Managing focus, text selection, or media playback.
- Triggering imperative animations.
- Integrating with third-party DOM libraries.
- *Avoid using refs for anything that can be done declaratively.*
### How to create refs?
Refs are created using React.createRef() and attached to React elements via the ref attribute. Refs are commonly assigned to an instance property when a component is constructed so they can be referenced throughout the component.
```
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.myRef = React.createRef();
  }
  render() {
    return <div ref={this.myRef} />;
  }
}
```
### What are forward refs?
By default, you may not use the ref attribute on function components because they don’t have instances. If you want to allow people to take a ref to your function component, you can use forwardRef. Ref forwarding is an opt-in feature that lets some components take a ref they receive, and pass it further down (in other words, “forward” it) to a child.
```
const FancyButton = React.forwardRef((props, ref) => (
  <button ref={ref} className="FancyButton">
    {props.children}
  </button>
));

// You can now get a ref directly to the DOM button:
const ref = React.createRef();
<FancyButton ref={ref}>Click me!</FancyButton>;
```
- We create a React ref by calling React.createRef and assign it to a ref variable.
- We pass our ref down to <FancyButton ref={ref}> by specifying it as a JSX attribute.
- React passes the ref to the (props, ref) => ... function inside forwardRef as a second argument.
- We forward this ref argument down to <button ref={ref}> by specifying it as a JSX attribute.
- When the ref is attached, ref.current will point to the <button> DOM node.
### Which is preferred option with in callback refs and findDOMNode()?
- findDOMNode is an escape hatch used to access the underlying DOM node. In most cases, use of this escape hatch is discouraged because it pierces the component abstraction. It has been deprecated in StrictMode.
### Why are String Refs legacy?
 > string refs have some issues, are considered legacy, and are likely to be removed in one of the future releases.
 > String refs could never be implemented in user space (callbacks can; just have the component call the callback). The ramifications of this are far-reaching. For instance, if you wanted to create a HOC (Higher Order Component) that transparently wraps another component, you could forward all the props... but you couldn't forward a string ref. Or if you wanted a parent and a grandparent to both have a ref to a component, callback refs allow you to wrap the callback and pass it down, but string refs do not.
> - String refs are not composable. A wrapping component can’t “snoop” on a ref to a child if it already has an existing string ref. On the other hand, callback refs don’t have a single owner, so you can always compose them.
> - String refs don’t work with static analysis like Flow. Flow can’t guess the magic that framework does to make the string ref “appear” on this.refs, as well as its type (which could be different). Callback refs are friendlier to static analysis.
> - The owner for a string ref is determined by the currently executing component. This means that with a common “render callback” pattern (e.g. <DataTable renderRow={this.renderRow} />), the wrong component will own the ref (it will end up on DataTable instead of your component defining renderRow).
> - String refs force React to keep track of currently executing component. This is problematic because it makes react module stateful, and thus causes weird errors when react module is duplicated in the bundle.
### What is Virtual DOM?
A virtual DOM is a lightweight JavaScript representation of the Document Object Model used in declarative web frameworks such as React, Vue.js, and Elm. Updating the virtual DOM is comparatively faster than updating the actual DOM.
### How Virtual DOM works?
when there is a update in the virtual DOM, react compares the virtual DOM with a snapshot of the virtual DOM taken right before the update of the virtual DOM.

With the help of this comparison React figures out which components in the UI needs to be updated. This process is called diffing. The algorithm that is used for the diffing process is called as the diffing algorithm.

Once React knows which components has been updated, then it replaces the original DOM nodes with the updated DOM node.
### What is the difference between Shadow DOM and Virtual DOM?
The only thing which is common for both is that they help with performance issues. Both create a separate instance of the Document Object Model; besides this, both concepts are different. Virtual DOM is creating a copy of the whole DOM object, and Shadow DOM creates small pieces of the DOM object which has their own, isolated scope for the element they represent.
### What is React Fiber?
React Fiber is a concept of ReactJS that is used to render a system faster and smoother. After certain changes who is the next element to render the system called reconciler. This algorithm helps to compare two DOM trees and diff them. React fiber helps to do it better.
React Fiber is a completely backward-compatible rewrite of the old reconciler. This new reconciliation algorithm from React is called Fiber Reconciler. The name comes from fiber, which it uses to represent the node of the DOM tree.
### What is the main goal of React Fiber?
The main goals of the Fiber reconciler are incremental rendering, better or smoother rendering of UI animations and gestures, and responsiveness of the user interactions. The reconciler also allows you to divide the work into multiple chunks and divide the rendering work over multiple frames. It also adds the ability to define the priority for each unit of work and pause, reuse, and abort the work.

Some other features of React include returning multiple elements from a render function, supporting better error handling(we can use the componentDidCatch method to get clearer error messages), and portals.

While computing new rendering updates, React refers back to the main thread multiple times. As a result, high-priority work can be jumped over low-priority work. React has priorities defined internally for each update.
### What are controlled components?
Uncontrolled component and Controlled component are terms used to describe React components that render HTML form elements.
> A controlled component is a component that renders form elements and controls them by keeping the form data in the component's state. In a controlled component, the form element's data is handled by the React component (not DOM) and kept in the component's state. A controlled component basically overrides the default behavior of the HTML form elements.
```
const { useState } from 'react';
function Controlled () {
  const [email, setEmail] = useState();
  const handleInput = (e) => setEmail(e.target.value);
  return <input type="text" value={email} onChange={handleInput} />;
}
```
### What are uncontrolled components?
> An uncontrolled component is a component that renders form elements, where the form element's data is handled by the DOM (default DOM behavior). To access the input's DOM node and extract its value you can use a ref.
```
const { useRef } from 'react';
function Example () {
  const inputRef = useRef(null);
  return <input type="text" defaultValue="bar" ref={inputRef} />
}
```
### What is the difference between createElement and cloneElement?
![Capture](https://user-images.githubusercontent.com/71145709/172849445-54053247-f568-4dcd-bd71-d17193bf120c.PNG)<br />
### What is Lifting State Up in React?
In React, sharing state is accomplished by moving it up to the closest common ancestor of the components that need it. This is called “lifting state up”. We will remove the local state from the child and move it into the closest common ancestor instead.
There should be a single “source of truth” for any data that changes in a React application. Usually, the state is first added to the component that needs it for rendering. Then, if other components also need it, you can lift it up to their closest common ancestor. Instead of trying to sync the state between different components, you should rely on the top-down data flow.
### What are the different phases of component lifecycle?
In ReactJS, the development of each component involves the use of different lifecycle methods. All the lifecycle methods used to create such components, together constitute the component’s lifecycle. They are defined as a series of functions invoked in various stages of a component. Each phase of the lifecycle components includes some specific lifecycle methods related to that particular phase. There are primarily 4 phases involved in the lifecycle of a reactive component, as follows.
- Initializing
- Mounting
- Updating
- Unmounting
### What are the lifecycle methods of React?
- getDefaultProps()
- getInitialState()
- componentWillMount()
- componentDidMount()
- componentWillReceiveProps()
- shouldComponentUpdate()
- componentWillUpdate()
- componentDidUpdate()
### What are Higher-Order components?
A higher-order component (HOC) is an advanced technique in React for reusing component logic.
Concretely, a higher-order component is a function that takes a component and returns a new component.
### How to create props proxy for HOC component?
You can add/edit props passed to the component using props proxy pattern like this:
```
function HOC(WrappedComponent) {
  return class Test extends Component {
    render() {
      const newProps = {
        title: 'New Header',
        footer: false,
        showFeatureX: false,
        showFeatureY: true,
      };
      return <WrappedComponent {...this.props} {...newProps} />;
    }
  };
}
```
### What is context?
Context provides a way to pass data through the component tree without having to pass props down manually at every level.
Context is designed to share data that can be considered “global” for a tree of React components, such as the current authenticated user, theme, or preferred language.
### What is children prop?
props.children represents the content between the opening and the closing tags when invoking/rendering a component.
 props. children is a special prop, automatically passed to every component, that can be used to render the content included between the opening and closing tags when invoking a component.
### How to write comments in React?
We can write comments in React using the double forward-slash // or the asterisk format /* */, similar to regular JavaScript.
### What is the purpose of using super constructor with props argument?
super() is used to call the parent constructor. super(props) would pass props to the parent constructor.
### What is reconciliation?
React provides a declarative API so that you don’t have to worry about exactly what changes on every update. This makes writing applications a lot easier, but it might not be obvious how this is implemented within React.
Reconciliation is the process through which React updates the DOM. When a component’s state changes, React has to calculate if it is necessary to update the DOM. It does this by creating a virtual DOM and comparing it with the current DOM.
### How to set state with a dynamic key name?
inputChangeHandler: function ({ target: { id, value }) {
    this.setState({ [id]: value });
}
### What would be the common mistake of function being called every time the component renders?
You need to make sure that function is not being called while passing the function as a parameter.
```
render() {
// Wrong: handleClick is called instead of passed as a reference!
return <button onClick={this.handleClick()}>{'Click Me'}</button>
}
render() {
// Correct: handleClick is passed as a reference!
return <button onClick={this.handleClick}>{'Click Me'}</button>
}
```
### Is lazy function supports named exports?
lazy() does not support using named exports for React components. If you wish to use named exports containing React components, you need to reexport them as default exports in separate intermediate modules.
### Why React uses className over class attribute?
The only reason behind the fact that it uses className over class is that the class is a reserved keyword in JavaScript and since we use JSX in React which itself is the extension of JavaScript, so we have to use className instead of class attribute.
### What are fragments?
A common pattern in React is for a component to return multiple elements. Fragments let you group a list of children without adding extra nodes to the DOM.
```
render() {
  return (
    <React.Fragment>
      <ChildA />
      <ChildB />
      <ChildC />
    </React.Fragment>
  );
}
```
### What are portals in React?
Portals provide a first-class way to render children into a DOM node that exists outside the DOM hierarchy of the parent component.
````ReactDOM.createPortal(child, container)````
The first argument (child) is any renderable React child, such as an element, string, or fragment. The second argument (container) is a DOM element.
### What are stateless components?
Stateless components are those components which don't have any state at all, which means you can't use this. setState inside these components. It is like a normal function with no render method. It has no lifecycle, so it is not possible to use lifecycle methods such as componentDidMount and other hooks.
### What are stateful components?
In React, a stateful component is a component that holds some state. Stateless components, by contrast, have no state. Note that both types of components can use props.
### How to apply validation on props in React?
React JS has an inbuilt feature for validating props data type to make sure that values passed through props are valid. React components have a property called propTypes which is used to setup data type validation.
````
class Component extends React.Component {
  render() {}
}
Component.propTypes = {/* definition goes here*/};
````
### What are the advantages of React?
- It is composable.
- Reusable Components
- It is declarative.
- It is simple.
- SEO friendly.
- Fast, efficient, and easy to learn.
- Scope for Testing the Codes
- The Support of Handy Tools
- Performance Enhancement
### What are the limitations of React?
- Lack of Proper Documentation
- Development Speed
- JSX as a barrier
- only UI covered
### What are error boundaries in React v16?
In the past, JavaScript errors inside components used to corrupt React’s internal state and cause it to emit cryptic errors on next renders. These errors were always caused by an earlier error in the application code, but React did not provide a way to handle them gracefully in components, and could not recover from them.
To solve this problem for React users, React 16 introduces a new concept of an “error boundary”. Error boundaries are React components that catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI instead of the component tree that crashed.
### How error boundaries handled in React v15?
React v15 provided very basic support for error boundaries using unstable_handleError method. It has been renamed to componentDidCatch in React v16.
### What are the recommended ways for static type checking?
Static type checkers like Flow and TypeScript identify certain types of problems before you even run your code. They can also improve developer workflow by adding features like auto-completion.
Normally we use PropTypes library (React.PropTypes moved to a prop-types package since React v15.5) for type checking in the React applications. For large code bases, it is recommended to use static type checkers such as Flow or TypeScript, that perform type checking at compile time and provide auto-completion features.
### What is the use of react-dom package?
The react-dom package provides DOM-specific methods that can be used at the top level of your app and as an escape hatch to get outside the React model if you need to.
### What is the purpose of render method of react-dom?
This is one of the most important methods of ReactDOM. This function is used to render a single React Component or several Components wrapped together in a Component or a div element. This function uses the efficient methods of React for updating the DOM by being able to change only a subtree, efficient diff methods, etc.
`ReactDOM.render(element, container, callback)`
### What is ReactDOMServer?
The ReactDOMServer object enables you to render components to static markup. Typically, it’s used on a Node server.
These methods are only available in the environments with Node.js Streams:
- renderToPipeableStream()
- renderToNodeStream() (Deprecated)
- renderToStaticNodeStream()
- renderToReadableStream()
- renderToString()
- renderToStaticMarkup()
### How to use InnerHtml in React?
The dangerouslySetInnerHTML attribute is React's replacement for using innerHTML in the browser DOM. Just like innerHTML, it is risky to use this attribute considering cross-site scripting (XSS) attacks. You just need to pass a __html object as key and HTML text as value.
````
function createMarkup() {
  return { __html: 'First &middot; Second' };
}
function MyComponent() {
  return <div dangerouslySetInnerHTML={createMarkup()} />;
}
````
### How to use styles in React?
React Components can add styling in the following ways:

- Add the Global Styles to “index.html” File
- Adding Inline Style to React Component Elements
- CSS Modules
- Styled-components 💅 (a library)
### How events are different in React?
### What will happen if you use setState in constructor?
> What setState essentially does is to run a bunch of logic you probably don't need in the constructor. When you go state = {foo : "bar"} you simply assign something to the javascript object state, like you would any other object. (That's all state is by the way, just a regular object local to every component).
> When you use setState(), then apart from assigning to the object state react also rerenders the component and all its children. Which you don't need in the constructor, since the component hasn't been rendered anyway.
### What is the impact of indexes as keys?
answer could be found in the Docs of React
> We don’t recommend using indexes for keys if the order of items may change. This can negatively impact performance and may cause issues with component state. Check out Robin Pokorny’s article for an in-depth explanation on the negative impacts of using an index as a key. If you choose not to assign an explicit key to list items then React will default to using indexes as keys.
> If we are not adding /removing items from list then it is fine to use index as keys else it will be good to use some id which uniquely identifies the item. Reason is if you add or remove some items from the list, indexes change for older items and react can get confused which items are changed.
### Is it good to use setState() in componentWillMount() method?
> Using setState inside componentWillMount() is fine: "The componentWillMount() is a chance for us to handle configuration, update our state, and in general prepare for the first render. At this point, props and initial state are defined. We can safely query this.props and this.state, knowing with certainty they are the current values. This means we can start performing calculations or processes based on the prop values."
taken from here. "calling setState() synchronously in componentWillMount() method will not trigger an extra rendering".
> However It is not recommended to use asynchronous actions inside componentWillMount().Well, when you do an async request in the constructor / componentWillMount you do it before render gets called, by the time the async operation has finished the render method most probably already finished and no point to set the "initial state" at this stage is it?.
### What will happen if you use props in initial state?
> If the props on the component are changed without the component being refreshed, the new prop value will never be displayed because the constructor function will never update the current state of the component. The initialization of state from props only runs when the component is first created.
let's see a few ways to fix it.
**Parent Component Needs The Value**
> In case if the parent component needs the value, for example to send it to the API, we can leave the state handling in the component and just pass the value and the update function as props.
**Parent Component Doesn't Need The Value**
> If the parent component doesn't need the value, why would we leave it there to unnecessarily re-render the entire parent component?try moving the state and update function to the child component
> Destroy and re-create the child component when the prop changes.We can also use the prop as a key to create a new instance of the ChildComponent each time it changes to reset the state.
### How do you conditionally render components?
In React, you can create distinct components that encapsulate behavior you need. Then, you can render only some of them, depending on the state of your application.
- use if -else
- use Inline If with Logical && Operator
- use Inline If-Else with Conditional Operator (ternary)
You can use variables to store elements. This can help you conditionally render a part of the component while the rest of the output doesn’t change.
### Why we need to be careful when spreading props on DOM elements?
You should avoid spreading properties into a DOM element as it adds unknown HTML attribute, which is unnecessary and a bad practice.
```
const CommentsText = props => {
    return (
      <div {...props}>
        {props.text}
      </div>
    );
  };
```
Instead of spreading props, you can set specific attributes:
```
const CommentsText = props => {
    return (
      <div specificAttr={props.specificAttr}>
        {props.text}
      </div>
    );
};
```
### How you use decorators in React?
### How do you memoize a component?
### How you implement Server-Side Rendering or SSR?
### How to enable production mode in React?
### What is the lifecycle methods order in mounting?
* render => componentWillMount => componentDidMount => componentWillUpdate => componentDidUpdate => componentWillUnmount
* for mounting: constructor call, then it renders, then calls componentDidMount.
*
### What are the lifecycle methods going to be deprecated in React v16?
The methods that are deprecated are as follows:
- componentWillMount
All the legacy use cases are covered in the constructor. This is renamed as UNSAFE_componentWillMount.
- componentWillReceiveProps
The new static method getDerivedStateFromProps is safe rewrite for this method and covers all the use cases of componentWillReceiveProps. The new name for this method is UNSAFE_componentWillReceiveProps.
- componentWillUpdate
The new method getSnapshotBeforeUpdate is safe rewrite for this method and covers all the use cases of componentWillUpdate.
The new name for this method is UNSAFE_componentWillUpdate.
### What is the purpose of getDerivedStateFromProps() lifecycle method?
### What is the purpose of getSnapshotBeforeUpdate() lifecycle method?
### Do Hooks replace render props and higher order components?

# Refrences

* https://reactjs.org/tutorial/tutorial.html
* https://stackoverflow.com/
* https://www.geeksforgeeks.org/
* https://iq.js.org/
* https://www.blog.duomly.com/
* https://www.codementor.io/
