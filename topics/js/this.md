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

## TODO
