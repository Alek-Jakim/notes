## TypeScript with React

---

### Basic Types

```javascript
  const name: string = "Alek";
  const age: number = 28;
  const isMarried: boolean = true;

  const getName = (name: string):number =>  {
    console.log(name);
    return 5
  }
```

### Functional Component
```javascript
const Person: FC = () => {
    return (
        <div>Person</div>
    )
}
export default Person
```

### Props

```javascript
import React from 'react'

interface Props {
    email: string,
    name: string,
    age: number,
    // question mark means it is optional
    getName?: () => string

}

// This is how you can destructure the props
const Person = ({ email, name, age }: Props) => {
    return (
        <div>
            <div>
                <p>Name: {name}</p>
                <p>Age: {age}</p>
                <p>Email: {email}</p>
            </div>
        </div>
    )
}

export default Person
```

```javascript
import React, { FC } from 'react'

interface Props {
    email: string,
    name: string,
}

// This is how you can define props for a functional component
const Person: FC<Props> = ({email, name}) => {
    return (
        <div>
                {// code}
        </div>
    )
}

export default Person
```

### useState

```javascript
import React, { ChangeEvent, FC, useState } from 'react'

    const [country, setCountry] = useState<string | null>(null)

    <input type="text" placeholder="Write down your country..." onChange={(e: ChangeEvent<HTMLInputElement>) => setCountry(e.target.value)} /
```

### Enums/Types

```javascript
/*
Enums should ideally be used in situations where there are distinct values that can be seen as constants, like seven days of the week
*/


enum HairColor {
    Blonde = "Your hair is blonde, good for you",
    Brown = "Cool hair color",
    Pink = "Wow pink so crazy"
}

interface Person {
    name: string,
    age: number,
    hairColor: HairColor
}

<p>{HairColor.Blonde}</p>
```


[Context API Snippet](./react-ts-context.md)

### Context API

```javascript
import React, { FC, createContext } from "react"

interface AppContextInterface {
  name: string;
  age: number;
  country: string;
}

const AppContext = createContext<AppContextInterface | null>(null);


const App: FC = () => {

  const contextValue: AppContextInterface = {
    name: "Alek",
    age: 20,
    country: "Macedonia"
  }

  return (
    <AppContext.Provider value={contextValue}>
      <div>
        <h1>Name: {contextValue.name}</h1>
        <h1>Age: {contextValue.age}</h1>
        <h1>Country: {contextValue.country}</h1>
      </div>
    </AppContext.Provider >
  )
}

export default App
```

---

## Basic Prop Types Examples

A list of TypeScript types you will likely use in a React+TypeScript app:

```javascript
type AppProps = {
  message: string;
  count: number;
  disabled: boolean;
  /** array of a type! */
  names: string[];
  /** string literals to specify exact string values, with a union type to join them together */
  status: "waiting" | "success";
  /** any object as long as you dont use its properties (NOT COMMON but useful as placeholder) */
  obj: object;
  obj2: {}; // almost the same as `object`, exactly the same as `Object`
  /** an object with any number of properties (PREFERRED) */
  obj3: {
    id: string;
    title: string;
  };
  /** array of objects! (common) */
  objArr: {
    id: string;
    title: string;
  }[];
  /** a dict object with any number of properties of the same type */
  dict1: {
    [key: string]: MyTypeHere;
  };
  dict2: Record<string, MyTypeHere>; // equivalent to dict1
  /** any function as long as you don't invoke it (not recommended) */
  onSomething: Function;
  /** function that doesn't take or return anything (VERY COMMON) */
  onClick: () => void;
  /** function with named prop (VERY COMMON) */
  onChange: (id: number) => void;
  /** alternative function type syntax that takes an event (VERY COMMON) */
  onClick(event: React.MouseEvent<HTMLButtonElement>): void;
  /** an optional prop (VERY COMMON!) */
  optional?: OptionalType;
};
```

## Useful React Prop Type Examples

Relevant for components that accept other React components as props.

```javascript
export declare interface AppProps {
  children1: JSX.Element; // bad, doesnt account for arrays
  children2: JSX.Element | JSX.Element[]; // meh, doesn't accept strings
  children3: React.ReactChildren; // despite the name, not at all an appropriate type; it is a utility
  children4: React.ReactChild[]; // better, accepts array children
  children: React.ReactNode; // best, accepts everything (see edge case below)
  functionChildren: (name: string) => React.ReactNode; // recommended function as a child render prop type
  style?: React.CSSProperties; // to pass through style props
  onChange?: React.FormEventHandler<HTMLInputElement>; // form events! the generic parameter is the type of event.target
  //  more info: https://react-typescript-cheatsheet.netlify.app/docs/advanced/patterns_by_usecase/#wrappingmirroring
  props: Props & React.ComponentPropsWithoutRef<"button">; // to impersonate all the props of a button element and explicitly not forwarding its ref
  props2: Props & React.ComponentPropsWithRef<MyButtonWithForwardRef>; // to impersonate all the props of MyButtonForwardedRef and explicitly forwarding its ref
}
```

## Types or Interfaces?

Here's a helpful rule of thumb:

* always use `interface` for public API's definition when authoring a library or 3rd party ambient type definitions, as this allows a consumer to extend them via declaration merging if some definitions are missing.

* consider using `type` for your React Component Props and State, for consistency and because it is more constrained.

---

## Function Components

These can be written as normal functions that take a `props` argument and return a JSX element.

```javascript
// Declaring type of props - see "Typing Component Props" for more examples
type AppProps = {
  message: string;
}; /* use `interface` if exporting so that consumers can extend */

// Easiest way to declare a Function Component; return type is inferred.
const App = ({ message }: AppProps) => <div>{message}</div>;

// you can choose annotate the return type so an error is raised if you accidentally return some other type
const App = ({ message }: AppProps): JSX.Element => <div>{message}</div>;

// you can also inline the type declaration; eliminates naming the prop types, but looks repetitive
const App = ({ message }: { message: string }) => <div>{message}</div>;
```

---

## Hooks

Hooks are supported in @types/react from v16.8 up.

Type inference works very well for simple values:

```javascript
const [val, toggle] = React.useState(false);
// `val` is inferred to be a boolean
// `toggle` only takes booleans
```

Many hooks are initialized with null-ish default values, and you may wonder how to provide types. Explicitly declare the type, and use a union type:

```javascript
const [user, setUser] = React.useState<IUser | null>(null);

// later...
setUser(newUser);
```

You can also use type assertions if a state is initialized soon after setup and always has a value after:

```javascript
const [user, setUser] = React.useState<IUser>({} as IUser);

// later...
setUser(newUser);
```