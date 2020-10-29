## Redux

To use React Redux with your React app:

```bash
    npm install redux react-redux
```

You also need to set up a Redux store in the app.

### Store

A store holds the whole state tree of your application. The only way to change the state inside it is to dispatch an action on it.

A store is not a class. It's just an object with a few methods on it: 

* getState()
* dispatch(action)
* subscribe(listener)
* replaceReducer(nextReducer)

To create it, pass your root reducing function to createStore.

```javascript
import React from 'react'
import ReactDOM from 'react-dom';
import App from './App';
import { createStore } from 'redux'


//ACTION 
const increment = () => {
    return {
        type: 'INCREMENT'
    }
}

const decrement = () => {
    return {
        type: 'DECREMENT'
    }
}

//REDUCER
const counter = (state = 0, action) => {
    switch (action.type) {
        case "INCREMENT":
            return state += 1;
        case "DECREMENT":
            return state -= 1;
    }
}

//STORE -> Globalized State
let store = createStore(counter);

store.subscribe(() => {
    console.log(store.getState());
})

store.dispatch(increment()) // console logs 1

ReactDOM.render(<App />, document.getElementById('root'));
```