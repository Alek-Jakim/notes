# React Hooks

Hooks let you use state and other React features without writing a class.

Hooks are functions that let you “hook into” React state and lifecycle features from function components. Hooks don’t work inside classes — they let you use React without classes.

Hooks are JavaScript functions, but they impose two additional rules:

* Only call Hooks at the top level. Don’t call Hooks inside loops, conditions, or nested functions.

* Only call Hooks from React function components. Don’t call Hooks from regular JavaScript functions. (There is just one other valid place to call Hooks — your own custom Hooks.)

## 1. `useState()`

* Returns a stateful value, and a function to update it.

* During the initial render, the returned state (state) is the same as the value passed as the first argument (initialState).

* The setState function is used to update the state. It accepts a new state value and enqueues a re-render of the component.

* During subsequent re-renders, the first value returned by useState will always be the most recent state after applying updates.


```javascript
// 1. Importing useState
import React, { useState } from 'react'

function App() {
  // 2. Destructuring useState
  // naming our: state variable 'count' & update function 'setCount'
  let [count, setCount] = useState(0);
  // 3. useState allows us to pass in the starting value, here it is 0

 // below we are:
 // - displaying count with {count}
 // - updating count with setCount when the button is clicked (more info below code)
  return (
    <div className="App">
        <p>You clicked {count} times</p>
      <button onClick={() => setCount(prevCount => prevCount + 1)}>
                Click Me
            </button>
    </div>
  );
}

export default App;
```

---
## 2. `useEffect()`

* A functional React component uses props and/or state to calculate the output. If the functional component makes calculations that don’t target the output value, then these calculations are named side-effects.

* `useEffect` is a hook that manages side-effects in functional React components. Examples of side-effects are fetch requests, manipulating DOM directly, using timer functions like `setTimeout()`, and more.


```javascript
import React, { useState, useRef, useEffect } from "react";
function EffectsDemoNoDependency() {
  const [title, setTitle] = useState("default title");
  const titleRef = useRef();
  useEffect(() => {
    console.log("useEffect");
    document.title = title;
  });
  const handleClick = () => setTitle(titleRef.current.value);
  console.log("render");
  return (
    <div>
      <input ref={titleRef} />
      <button onClick={handleClick}>change title</button>
    </div>
  );
}
```

* The component rendering and side-effect logic are independent. It would be a mistake to perform side-effects directly in the body of the component, which is primarily used to compute the output.

* `dependencies` argument of `useEffect(callback, dependencies)` lets you control when the side-effect runs. When dependencies are:

    * Not provided: the side-effect runs after every rendering.

    * An empty array []: the side-effect runs once after the initial rendering.

    * Has props or state values [prop1, prop2, ..., state1, state2]: the side-effect runs only when any depenendecy value changes.


* Some side-effects need cleanup: close a socket, clear timers.

* If the callback of useEffect(callback, deps) returns a function, then useEffect() considers this as an effect cleanup:

```javascript
useEffect(() => {
  // Side-effect...
  return function cleanup() {
    // Side-effect cleanup...
  };
}, dependencies);
```
---
## 3. `useRef()`

* `useRef` is one of the standard hooks provided by React. It will return an object that you can use during the whole lifecycle of the component. 

* The main use case for the `useRef` hook is to access a DOM child directly. I’ll show exactly how to do that in another section. 

* Although accessing the DOM is the main use case, it doesn’t mean it’s the only one! `useRef` can also be very useful to hold a mutable value across different renders of your component. 

```javascript
import { useEffect, useRef } from "react";

export default function App() {
  // create a ref
  const divElement = useRef();

  // trigger on the first render of the component 
  useEffect(() => {
    // get the height of the div element
    console.log(
      "The height of the div is: ", divElement.current.offsetHeight
    );
  }, []);

  return (
    <div ref={divElement}>
      <h1>Learn about useRef!</h1>
    </div>
  );
}
```

* **A ref changing value doesn’t trigger a re-render!** It is the opposite behavior of what happens when using `useState`.

For example, in the code below, the issue is that clicking the button increases the variable counter as expected, but it doesn’t trigger a re-render so we see nothing on the screen: 

```javascript
import { useRef } from "react";

export default function App() {
  // create a ref
  const counter = useRef(0);

  // increase the counter by one
  const handleIncreaseCounter = () => {
    counter.current = counter.current + 1;
  };

  return (
    <div>
      <h1>Learn about useRef!</h1>
      <h2>Value: {counter.current}</h2>
      <button onClick={handleIncreaseCounter}>
        Increase counter
      </button>
    </div>
  );
}
```

* **It is useless to add a ref to a dependency array!** Adding a ref to a dependency array (for example the one of a `useEffect` hook) will not trigger the callback! This is also a very common error. 

* Most of the time, if you want to persist state across re-renders of your components you should be using `useState` instead of `useRef`. 

