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

---

## Public & Private Fields; Private Methods

### Public Fields

- Public fields provide a straightforward way to define properties on class instances without needing to use the constructor for initialization. They are useful for setting default values & initializing simple properties.

```javascript
class Person {
  // Public field
  name = "John Doe";

  // Public field
  age = 30;

  greet() {
    console.log(
      `Hello, my name is ${this.name} and I am ${this.age} years old.`
    );
  }
}
```

### Private Fields & Methods

- Private fields & methods should be used when you need to manage sensitive data (like the account balance) securely. We use the `#` symbol to declare that a field/method is private.

```javascript
class BankAccount {
  // Private field - Protects #balance from direct external modification.
  #balance = 0;

  constructor(accountHolder) {
    this.accountHolder = accountHolder;
  }

  deposit(amount) {
    if (this.#isValidAmount(amount)) {
      this.#balance += amount;
      this.#logTransaction("deposit", amount);
    }
  }

  withdraw(amount) {
    if (this.#isValidAmount(amount) && this.#balance >= amount) {
      this.#balance -= amount;
      this.#logTransaction("withdraw", amount);
    } else {
      console.log("Insufficient funds or invalid amount.");
    }
  }

  getBalance() {
    return this.#balance;
  }

  // Ensures #isValidAmount is used internally to validate transactions
  #isValidAmount(amount) {
    return amount > 0;
  }

  // Keeps transaction logs private and internal
  #logTransaction(type, amount) {
    console.log(
      `${type} of ${amount} was successful. Current balance: ${this.#balance}`
    );
  }
}
```

---

## Static Initialization Block

- These blocks are useful when you need to perform more complex initialization than what can be done with simple assignments.

- It's defined using the `static` keyword followed by a pair of curly braces `{}`.

```javascript
class Configuration {
  static settings = {};

  static {
    // Complex initialization logic
    this.settings.apiKey = process.env.API_KEY || "default-api-key";
    this.settings.dbConnectionString =
      process.env.DB_CONNECTION_STRING || "default-db-connection-string";
  }
}
```

- A good use case for static initialization blocks is when you need to initialize static properties based on some complex logic, such as fetching configuration from environment variables, performing computations, or setting up static resources that require multiple steps.

```javascript
class AppConfig {
  static config = {};

  static {
    // Initialize configuration settings
    this.config = {
      apiEndpoint: process.env.API_ENDPOINT || "https://default.api.endpoint",
      dbHost: process.env.DB_HOST || "localhost",
      dbPort: parseInt(process.env.DB_PORT, 10) || 5432,
      featureFlags: {
        enableNewFeature: process.env.ENABLE_NEW_FEATURE === "true",
      },
    };

    // Additional initialization logic if needed
    if (!this.config.apiEndpoint.startsWith("https")) {
      console.warn("API endpoint should use HTTPS");
    }
  }
}

console.log(AppConfig.config);
```

[More on JS classes](https://www.freecodecamp.org/news/javascript-classes-how-they-work-with-use-case/)
