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

---

### Prototypes

Every JS object has its own special property called Prototype. That Prototype is itself an object, which can have its own Prototype (aka. Prototype Chain).

```javascript
// Example 1 - printInfo lives on the Prototype, so all instances of User get it from there
class User {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  printInfo() {
    console.log(`${this.name} - ${this.age}`);
  }
}
const elton = new User("Elton", 54);
const john = new User("john", 40);

console.log(elton.printInfo === john.printInfo); // true

// Example 2 - each instance has its own printInfo method on it

function User(name, age) {
  this.name = name;
  this.age = age;

  this.printInfo = function () {
    console.log(`${this.name} - ${this.age}`);
  };
}
console.log(elton.printInfo === john.printInfo); // false

// Or we can just put it on the Prototype directly - this is one of the things that the `new` keyword does (point 2).
User.prototype.printInfo = function () {
  console.log(`${this.name} - ${this.age}`);
};
```

---

### Prototype Chain

When the JavaScript engine looks for a property or method in an object and cannot find it, it would go to its prototype and look for it there, if it does not find it, it would go to the prototype of that prototype and continue to go down the **prototype chain** until it finds it.

```javascript
const grandparent = {
  greet() {
    console.log("Hello");
  },
};

const parent = {
  name: "John",
  introduce: function () {
    console.log(`My name is ${self.name ? self.name : "Roland"}`);
  },
  __proto__: grandparent,
};

const child = {
  age: 10,
  __proto__: parent,
};

console.log(child.name); // John
child.greet(); // Hello
console.log(child.__proto__); // parent object
console.log(child.__proto__.__proto__); // grandparent object
console.log(child.__proto__.__proto__.__proto__); // object object
```
