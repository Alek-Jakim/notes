## Design Patterns

### Module Pattern

- A design pattern used to encapsulate and organize related functionality into a single object or function.

- Helps prevent global scope pollution and provides a way to create private variables and methods, exposing only the parts of an object that you want to be publicly accessible.

- It allows you to expose a public API while keeping internal variables and methods private. This is done by returning an object that contains references to public methods, but the internal data is kept hidden within the closure.

- **When to use it**:

1. Encapsulating logic: When you want to group related methods and variables together, keeping internal details private.

2. Organizing code: Useful in large applications where code organization is key.

3. Preventing global namespace pollution: Helps avoid creating multiple global variables, which can cause conflicts in the global scope.

```javascript
const CounterModule = (function () {
  // Private variable
  let count = 0;

  // Private method
  function logCount() {
    console.log(`Current count: ${count}`);
  }

  // Public API
  return {
    increment: function () {
      count++;
      logCount();
    },
    decrement: function () {
      count--;
      logCount();
    },
    reset: function () {
      count = 0;
      logCount();
    },
    getCount: function () {
      return count;
    },
  };
})();
```

---

### Singleton Pattern

- Ensures that a class or object has only one instance throughout the lifecycle of an application.

- Particularly useful when you need a single point of control, such as managing shared resources like a database connection, a global configuration object, or logging.

- **When to use it**:

1. Shared resources: When there’s a resource that should be shared across the entire application (e.g., database connection).

2. Global state management: To manage a global state in scenarios where you only need one instance to exist (e.g., a user session manager).

3. Limiting instantiation: When creating multiple instances would be inefficient or unnecessary.

```javascript
// Example 1
const SingletonLogger = (function () {
  let instance;

  function createInstance() {
    return {
      log: function (message) {
        console.log(`Log: ${message}`);
      },
    };
  }

  return {
    getInstance: function () {
      if (!instance) {
        instance = createInstance();
      }
      return instance;
    },
  };
})();
```

```javascript
class ConfigurationManager {
  constructor() {
    if (ConfigurationManager.instance) {
      return ConfigurationManager.instance;
    }

    this.config = {};

    ConfigurationManager.instance = this;
  }

  set(key, value) {
    this.config[key] = value;
  }

  get(key) {
    return this.config[key];
  }
}

// Usage
const config1 = new ConfigurationManager();
const config2 = new ConfigurationManager();

config1.set("apiUrl", "https://api.example.com");
console.log(config2.get("apiUrl")); // https://api.example.com
console.log(config1 === config2); // true
```
