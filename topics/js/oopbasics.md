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

[More on JS classes](https://www.freecodecamp.org/news/javascript-classes-how-they-work-with-use-case/)
