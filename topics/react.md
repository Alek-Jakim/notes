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

This syntax is called JSX, and it is a syntax extension to JavaScript. We use it to describe what the UI should look like. JSX comes with the full power of JavaScript. JSX produces React “elements”. 

React separates concerns with loosely coupled units called “components” that contain both. 

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

## React Topics

### [Props and State](./react-course/props-state.md)

### [React Router](./react-course/router.md)

### [React Hooks](./react-course/hooks.md)
---
## CC

### [React Course](./react-course/course.md)

### [React Main](./react-course/react-master/react-main.md)

