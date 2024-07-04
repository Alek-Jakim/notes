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

## TODO
