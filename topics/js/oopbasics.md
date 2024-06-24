## Classes

- **Classes** in JS are syntactic sugar over the prototype-based inheritance model.

- A `constructor` is a special function that creates and initializes an object instance of a class. In JavaScript, a constructor gets called when an object is created using the new keyword.

- `printUserInfo` is an instance method. It belongs to the class prototype, which is inherited by all instances of the class.

```javascript
class User {
  constructor(name, email) {
    this.name = name;
    this.email = email;
  }

  printUserInfo() {
    console.log(this.name, this.email);
  }
}

const user1 = new User("John", "john123@gmail.com");
user.printUserInfo();
```

---

## Inheritance Basics

- **Inheritance** enables you to define a class that takes all the functionality from a parent class and allows you to add more.

- Not defining the `constructor` on the child class will automatically call it from the parent class.

- The `super()` function caller finds and invokes the parent class’s constructor() method. A `super()` function caller is valid only in a derived class’s constructor() method.

```javascript
class Sprite {
  constructor(image, pos = [0, 0]) {
    this.image = image;
    this.pos = pos;
  }

  draw() {
    console.log("Draw");
  }

  update() {
    console.log("Update");
  }

  print() {
    console.log("I am a sprite");
  }
}

class Player extends Sprite {
  constructor(image, pos, name) {
    super(image, pos);
    this.name = name;
  }

  // method overriding
  print() {
    console.log("I am the player");
  }

  move() {
    console.log("Move");
  }
}

const player = new Player("./path-to-image", [100, 200]);
const sprite = new Sprite("./path-to-image", [50, 100]);

player.update(); // Update
player.draw(); // Draw
player.print(); // I am the player
player.move(); // Move

sprite.move(); // Error - the move method exists only on the child class instances
```

---

## Static properties & methods

- Static properties can't be accessed on class instances, only on the class itself.

- Static methods are often utility functions, such as functions to create or clone objects.

```javascript
class Counter {
  // Static property to keep track of the count of instances
  static instanceCount = 0;

  constructor() {
    // Increment the count whenever a new instance is created
    Counter.instanceCount++;
  }

  // Static method to get the current count of instances
  static getInstanceCount() {
    return Counter.instanceCount;
  }

  // Static method to reset the count
  static resetInstanceCount() {
    Counter.instanceCount = 0;
  }
}
```

---

## Getters & Setters

- `get` & `set` are what are called _accessor properties_; basically functions that execute on getting and setting a value but look like regular properties.

- `get` is usefull when there are properties derived from other values.

```javascript
// Example 1
class Circle {
  constructor(radius) {
    this._radius = radius;
    this._diameter = radius * 2;
  }
}

const circle1 = new Circle(5);
// diameter is 10
circle1._radius = 10;
// diameter is still 10

// Example 2
class Circle {
  static allowedColors = new Set(["red", "green", "blue"]);

  constructor(radius, color) {
    this._radius = radius;
    this._color = color;
  }

  get diameter() {
    return this._radius * 2;
  }

  get color() {
    return this._color;
  }

  set color(newColor) {
    if (!Circle.allowedColors.has(newColor)) {
      throw new Error("Unknown color!");
    } else {
      this._color = newColor;
    }
  }
}

const circle2 = new Circle(5, "green");
// diameter is 10
circle1._radius = 10;
// diameter is now 20

circle2.color; // green
circle2.color = "red";
circle2.color; // red
circle2.color = "pink";
```

[More on JS classes](https://www.freecodecamp.org/news/javascript-classes-how-they-work-with-use-case/)
