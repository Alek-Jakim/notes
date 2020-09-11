## `null vs undefined`

Both null and undefined are special non-value values to represent nothingness.

Most programming languages use a single non-value value, which is often called null to represent that a reference type has no value associated with it, but JavaScript is special!

```javascript
// Welcome to the JavaScript universe.
// In the beginning, there was nothing.

console.log(universe); // ReferenceError: universe is not defined
alert("Universe was never created!");
```

In the above snippet, line 5(alert) never executes. Line 4 throws an error and halts the JavaScript execution right there. This is a subtle but critical detail.


```javascript
let universe;
console.log(universe); // undefined
```

In this snippet, `universe` is declared on line 1, but we haven’t assigned any “explicit” value to it. When we try to access its value on line 2, `undefined` is printed to the console.

If `uninitialized` were the word used for undefined, a lot of confusion would have been avoided

All that we have got now is an intention that we may create a universe in the future. It holds no value as of now. It’s not even an “explicit” empty value. It’s emptiness beyond emptiness.

`undefined` represents a lack of an explicitly assigned value in a variable or in other words, a missing value.

```javascript
let universe;

// Let's create a universe now
universe = {
  name: "JavaScript Universe!"
};

console.log(universe.name); // "JavaScript Universe!"
```

In this snippet, we create a new object and assign it to the universe variable. Now our universe variable has an object value.

The key takeaway here is that JavaScript assigns the primitive value `undefined` when a variable doesn’t have an explicitly assigned value.

### `null` - intentionally empty

```javascript
let universe = null;
```
`universe` is initialized “explicitly” with an empty value represented by null. It is a special value to represent it has no value.

null value = primitive value that represents the intentional absence of any object value.

Because JavaScript uses dynamic types, when a variable is declared and is not assigned a value, there is no way to differentiate it between the `primitive types` and the `object type`. So as per the specification `null` represents an absence of an object value.

JavaScript never implicitly assigns `null` to anything; programmers have to explicitly assign `null`.