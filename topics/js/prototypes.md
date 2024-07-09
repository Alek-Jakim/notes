## Prototypes & `new` keyword

### `new` Keyword

It basically does 4 things:

1. Creates an empty object.

2. Set the Prototype - The new object's internal [[Prototype]] property is set to the prototype property of the constructor function.

3. Execute the Constructor - The constructor function is called with the new object as its context (this). This is where properties and methods are typically assigned to the new object.

4. Return the New Object - If the constructor function explicitly returns an object, that object is returned as the result of the `new` expression. Otherwise, the newly created object is returned.

```javascript
// Step 1
let newObj = {};

// Step 2
newObj.__proto__ = ConstructorFunction.prototype;

// Step 3
ConstructorFunction.call(newObj, ...arguments);

// Example
function User(name, age) {
  this.name = name;
  this.age = age;
}

User.prototype.greet = function () {
  console.log(`${this.name} is ${this.age} years old.`);
};

const user = new User("John", 30);
user.greet();
```
