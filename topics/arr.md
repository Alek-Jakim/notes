## Arrays

Arrays are list-like objects whose prototype has methods to perform traversal and mutation operations.

* [Expense Tracker](expense-tracker.md)

* [Array Methods](./arrays/arr-methods.md)

##### Create an Array
```javascript
let fruits = ['Apple', 'Banana']

console.log(fruits.length)
// 2
```

##### Access Array Item Using Index
```javascript
let first = fruits[0]
// Apple

let last = fruits[fruits.length - 1]
// Access the last item of an array
```

##### Loop over an Array
```javascript
fruits.forEach(function(item, index, array) {
  console.log(item, index)
})
// Apple 0
// Banana 1
```




