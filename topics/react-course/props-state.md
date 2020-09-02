### Props

Props is short for properties and they are used to pass data between React components. React’s data flow between components is uni-directional (from parent to child only).

```javascript
class ParentComponent extends Component {    
    render() {    
        return (        
            <ChildComponent name="First Child" />    
        );  
    }
}

const ChildComponent = (props) => {    
    return <p>{props.name}</p>; 
};
```

### State

React has another special built-in object called state, which allows components to create and manage their own data. So unlike props, components cannot pass data with state, but they can create and manage it internally.

```javascript
class Test extends React.Component {    
    constructor() {    
        this.state = {      
            id: 1,      
            name: "test"    
        };  
    }    
    
    render() {    
        return (      
            <div>        
              <p>{this.state.id}</p>        
              <p>{this.state.name}</p>      
            </div>    
        );  
    }
}
```

State should not be modified directly, but it can be modified with a special method called `setState()`

```javascript
this.state.id = “2020”; // wrong

this.setState({         // correct  
    id: "2020"
});
```

A change in the state happens based on user-input, triggering an event, and so on. Also, React components (with state) are rendered based on the data in the state. State holds the initial information.

So when state changes, React gets informed and immediately re-renders the DOM – not the whole DOM, but only the component with the updated state. This is one of the reasons why React is fast.

The `setState( )` method triggers the re-rendering process for the updated parts. React gets informed, knows which part(s) to change, and does it quickly without re-rendering the whole DOM.

There are 2 important things to note:

* State shouldn’t be modified directly – the setState( ) should be used.

* State affects the performance of your app, and therefore it shouldn’t be used unnecessarily.

In the beginning, state could only be used in class components, not in functional components.

That’s why functional components were also known as stateless components. However, after the introduction of React Hooks, state can now be used both in class and functional components.

### Recap: 

* Components receive data from outside with props, whereas they can create and manage their own data with state

* Props are used to pass data, whereas state is for managing data

* Data from props is read-only, and cannot be modified by a component that is receiving it from outside

* State data can be modified by its own component, but is private (cannot be accessed from outside)

* Props can only be passed from parent component to child (unidirectional flow)

* Modifying state should happen with the `setState ( )` method