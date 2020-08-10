## React

React is a JavaScript library for building user interfaces. Learn what React is all about on our homepage or in the tutorial.

### Rendering Elements

Elements are the smallest building blocks of React apps. An element describes what you want to see on the screen:

```javascript
const element = <h1>Hello, world</h1>;
```

### JSX

```javascript
const element = <h1>Hello, world</h1>;
```

This syntax is called JSX, and it is a syntax extension to JavaScript. We use it to describe what the UI should look like. JSX comes with the full power of JavaScript.

JSX produces React “elements”. 

React embraces the fact that rendering logic is inherently coupled with other UI logic: how events are handled, how the state changes over time, and how the data is prepared for display.

Instead of artificially separating technologies by putting markup and logic in separate files, React separates concerns with loosely coupled units called “components” that contain both. 

React doesn’t require using JSX, but most people find it helpful as a visual aid when working with UI inside the JavaScript code. It also allows React to show more useful error and warning messages.

After compilation, JSX expressions become regular JavaScript function calls and evaluate to JavaScript objects.

This means that you can use JSX inside of if statements and for loops, assign it to variables, accept it as arguments, and return it from functions:

```javascript
function getGreeting(user) {
  if (user) {
    return <h1>Hello, {formatName(user)}!</h1>;
  }
  return <h1>Hello, Stranger.</h1>;
}
```

### Function and Class Components
The simplest way to define a component is to write a JavaScript function:

```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

This function is a valid React component because it accepts a single “props” (which stands for properties) object argument with data and returns a React element. We call such components “function components” because they are literally JavaScript functions.

You can also use an ES6 class to define a component:

```javascript
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

### [React Course](./react-course/course.md)
### [React Main](./react-course/react-master/react-main.md)