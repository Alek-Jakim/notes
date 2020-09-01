### Local Storage

We can access local storage via the `localStorage` global object. It works like an object, using key/value pairs.
It stores data under a specific key which we'll use to access it.

#### `setItem`

The `setItem` method is used to save data. It requires two arguments:
```javascript
localStorage.setItem('username', 'John');
```

#### `getItem`

The `getItem` method is used to get saved data out of local storage. It takes a single argument which is the `key.getItem`, and returns the value for that key.

```javascript
const name = localStorage.get('username')
console.log(name)
```

#### `removeItem`

The `removeItem` method is used to delete some data from local storage. It takes as its only argument the key for the data you want to remove.

```javascript
localStorage.removeItem('username')
```

#### `clear`

The `clear` method allows you to delete all the data stored in localStorage. It takes no arguments and returns nothing.

```javascript
localStorage.clear()
```