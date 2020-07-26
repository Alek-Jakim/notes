### Array Methods 
---
#### Adding and Removing

##### Add an item to the end of an Array

```javascript
//
let newLength = fruits.push('Orange')
// ["Apple", "Banana", "Orange"]
```

##### Add an item to the beginning of an Array

```javascript
let newLength = fruits.unshift('Strawberry') // add to the front
// ["Strawberry", "Banana"]
```

##### Remove an item from the end of an Array

```javascript
let last = fruits.pop() // remove Orange (from the end)
// ["Apple", "Banana"]
```
##### Remove an item from the beginning of an Array

```javascript
let first = fruits.shift() // remove Apple from the front
// ["Banana"]
```

-----
#### Other Useful Methods

1. Concat

* The concat() method is used to merge two or more arrays. This method does not change the existing arrays, but instead returns a new array.

```javascript
let fruits = ['apple', 'banana'];
let veggies = ['asparagus', 'brussel sprouts'];

let healthyFood = fruits.concat(veggies);

console.log(healthyFood) 
// [ 'apple', 'banana', 'asparagus', 'brussel sprouts' ]
```


2. Includes and IndexOf

* The Array.prototype.includes() method was introduced in ECMAScript 6. This method is used to find out whether the element is included in the array or not. It returns a boolean value — true or false.

* We use Array.prototype.indexOf() to find out whether the element is present in the array or not. But it doesn’t return a boolean. It returns the first index of the element found in the array, or it will return -1 (which represents that the element is not found).

```javascript
//includes()

let things = [
    'water',
    'fire',
    'wind',
    'earth',
    'plasma',
    'dark matter'
];

console.log(things.includes('dark matter')); //returns true
console.log(things.includes('Spirit')); //returns false


//indexOf()
console.log(things.indexOf('dark matter')); // returns 5
console.log(things.indexOf('God')); // returns - 1; It doesn't exist ;)
```

3. Reverse and Join

* The reverse() method reverses an array in place. The first array element becomes the last, and the last array element becomes the first. The reverse method transposes the elements of the calling array object in place, mutating the array, and returning a reference to the array.

* The join() method creates and returns a new **string** by concatenating all of the elements in an array (or an array-like object), separated by commas or a specified separator string. If the array has only one item, then that item will be returned without using the separator.

```javascript
let letters = ['c', 'b', 'a'];

console.log(letters.reverse()); // ['a', 'b', 'c' ]
console.log(letters.join('')); // abc
```


3. Slice

* The slice() method returns a shallow copy of a portion of an array into a new array object selected from start to end (end not included) where start and end represent the index of items in that array. The original array will not be modified.

```javascript
let animals = ['shark', 'salmon', 'whale', 'bear', 'lizard', 'tortoise'];

let swimmers = animals.slice(0, 3); //it includes the first index, but not the second (it goes up until 3)

let mammals = animals.slice(2, 4);

let reptiles = animals.slice(4);

console.log(swimmers); // [ 'shark', 'salmon', 'whale' ]
console.log(mammals); // [ 'whale', 'bear' ]
console.log(reptiles); // [ 'lizard', 'tortoise' ]
```

4. Splice

* The splice() method changes the contents of an array by removing or replacing existing elements and/or adding new elements in place.

##### Syntax
```javascript
let arrDeletedItems = array.splice(start[, deleteCount[, item1[, item2[, ...]]]])
```

```javascript
let animals = ['shark', 'salmon', 'whale', 'bear', 'lizard', 'tortoise'];

animals.splice(1, 0, 'octopus');

console.log(animals); // since the second index is 0, it doesn't delete anything

let deletedAnimals = animals.splice(3, 2);
console.log(deletedAnimals); // [ 'whale', 'bear' ]
console.log(animals); // [ 'shark', 'octopus', 'salmon', 'lizard', 'tortoise' ]
```

##### Parameters

* `start` - The index at which to start changing the array.
If greater than the length of the array, `start` will be set to the length of the array. In this case, no element will be deleted but the method will behave as an adding function, adding as many element as item[n*] provided.
If negative, it will begin that many elements from the end of the array. (In this case, the origin `-1`, meaning `-n` is the index of the nth last element, and is therefore equivalent to the index of `array.length - n`.)
If array.length + start is less than 0, it will begin from index 0.

* `deleteCount` (Optional) - An integer indicating the number of elements in the array to remove from `start`.
If `deleteCount` is omitted, or if its value is equal to or larger than `array.length - start` (that is, if it is equal to or greater than the number of elements left in the array, starting at start), then all the elements from `start` to the end of the array will be deleted. If `deleteCount` is 0 or negative, no elements are removed. In this case, you should specify at least one new element (see below).

* `item1, item2, ...` (Optional) - The elements to add to the array, beginning from `start`. If you do not specify any elements, `splice()` will only remove elements from the array.

* **Return Value** - An array containing the deleted elements.
If only one element is removed, an array of one element is returned.
If no elements are removed, an empty array is returned.

5. Sort (To be updated...)