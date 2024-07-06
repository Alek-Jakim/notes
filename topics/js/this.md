## `this`

### Global Objects & `this`

- When you call a function on "nothing", you call it on the global object. In the browser, that's typically the browser window. In NodeJS, that's global (where some Node utilities are).

```javascript
// here this is bound to the user object
const user = {
  username: "John123",
  email: "john123@gmail.com",
  userInfo() {
    console.log(`${this.username} - ${this.email}`);
  },
};

// this is bound to the window object
function whatIsThis() {
  console.log(`The value of this is ${this}`);
}
```

- A good rule for what the value of `this` is is "Left Of The Dot" rule.

```javascript
const user = {
  username: "John123",
  email: "john123@gmail.com",
  userInfo() {
    console.log(`${this.username} - ${this.email}`);
  },
};

// left of the dot is the user object, so this is bound to it.
user.userInfo();

function whatIsThis() {
  console.log(`The value of this is ${this}`);
}

// left of the dot is the window object (unless it's Node), so this is bound to it.
window.whatIsThis();

const dog = {
  name: "Lucky",
  age: 4,
  // this is now bound to the dog obj
  whatIsThis: whatIsThis,
};
```

---

### `this` and Classes

```javascript
// Normal object
const person = {
  name: "Mike",
  hobby: "reading",
  printInfo: function () {
    console.log(`${this}`);
  },
};

const personPrint = person.printInfo;

personPrint(); // either window obj (browser) or global obj(node)

// Class instance
class User {
  constructor(username) {
    this.username = username;
  }

  printSth() {
    console.log(`${this.username} - ${this}`);
  }
}
const user = new User("john");
user.printSth(); // john - user object

const printFunc = user.printSth;

printFunc(); // Error because this is undefined - also known as "losing the this context"
```

---

### `call`, `apply` and `bind` Methods

- `call` is a predefined JS method; allows you to call a function with a specific `this` value and arguments provided individually.

```javascript
// EXAMPLE 1
function logArguments() {
  // Convert arguments to a real array
  var argsArray = Array.prototype.slice.call(arguments);

  // Now we can use array methods on argsArray
  argsArray.forEach(function (arg) {
    console.log(arg);
  });
}

logArguments([1, 2, 3], "lalala", false);

// EXAMPLE 2
function takeDamage(damage) {
  this.hp -= damage;
}

class Entity {
  constructor(name, hp) {
    this.name = name;
    this.hp = hp ?? 10;
  }

  printInfo() {
    console.log(`${this.name} has ${this.hp} HP`);
  }
}

const player = new Entity("Player", 20);
const enemy = new Entity("Enemy");

takeDamage.call(player, 15);
player.printInfo(); // Player has 5 HP

takeDamage.call(enemy, 9);
enemy.printInfo(); // Enemy has 1 HP
```

- The `apply` method is similar to call, but it takes an array (or array-like object) of arguments instead of passing them individually.

```javascript
// Example 1
function sum(a, b, c) {
  return a + b + c;
}

const numbers = [1, 2, 3];

console.log(sum.call(null, 1, 2, 3)); // Output: 6
console.log(sum.apply(null, numbers)); // Output: 6

function findLargestNum() {
  return Math.max.apply(null, arguments);
}

// Example 2
function findLargestNum() {
  const args = Array.prototype.slice.call(arguments);
  if (args.length === 0) {
    throw new Error("No numbers were provided!");
  }
  return Math.max.apply(null, args);
}

console.log(findLargestNum()); // throws error
console.log(findLargestNum(28, 3, 19)); // 28
```

- The `bind` method returns a new function with a bound `this` value and optionally preset arguments. You can preset some arguments when binding and provide the rest when calling the bound function.

```javascript
// Method binding
const person = {
  name: "Alice",
  greet: function (greeting, punctuation) {
    console.log(greeting + ", " + this.name + punctuation);
  },
};
const boundGreet = person.greet.bind(person);
boundGreet("Hello", "!"); // Output: Hello, Alice!

// Partial application
function multiply(a, b) {
  return a * b;
}

const double = multiply.bind(null, 2);
console.log(double(5)); // Output: 10
```

When you do not directly call functions and instead JS calls them, a keyword `this` is created for you. This is the case for:

- Event Listeners
- Timers
- Callback functions (map, filter etc.)

```javascript
// Bind with event listeners
const user = {
  username: "john123",
  email: "john@gmail.com",
  printInfo: function () {
    console.log("This is ", this);
    console.log(`${this.username} - ${this.email}`);
  },
};

const btn = document.getElementById("btn");
btn.addEventListener("click", user.printInfo); // this points to the btn element; username & email are undefined
btn.addEventListener("click", user.printInfo.bind(user)); // this points to user

// Bind with timers
class Counter {
  constructor(count, incrementStep) {
    this.count = count ?? 0;
    this.incrementStep = incrementStep ?? 1;
  }

  incrementAndPrint() {
    console.log(this);
    console.log(this.count);

    this.count += this.incrementStep;
  }

  start() {
    setInterval(this.incrementAndPrint, 1000); //if you don't bind it, this will refer to the window object.
    setInterval(this.incrementAndPrint.bind(this), 1000); // shit works
  }
  // The other (better) way is to just use an arrow function

  //  start() {
  //   setInterval(() => {
  //     console.log(this.count);
  //     this.count += this.incrementStep;
  //   }, 1000);
  // }
}
const counter = new Counter(1, 2);
counter.start();
```

- Arrow functions don't make their own `this`.

```javascript
class User {
  constructor(name) {
    this.name = name;
  }

  printName() {
    setTimeout(function () {
      console.log(`Hello ${this.name}`);
    }, 1000);

    setTimeout(() => {
      console.log(`Hello ${this.name}`);
    }, 2000);
  }
}

new User("John").printName();
// Hello - this refers to window obj
// Hello John - - this refers to User instance
```

---

Key Takeaways:

- `this` is a keyword whose value is determined **only at the point of function execution**.

- If you're not the one calling the function (callback or sth), you need to make sure JS knows what the `this` context should be.

- There is a global context; what it is depends if you're using the browser(then it's the window) or Node (then it's the global obj).

## TODO
