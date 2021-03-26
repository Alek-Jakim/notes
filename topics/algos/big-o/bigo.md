## Big-O Notation

In plain words, Big O notation describes the complexity of your code using algebraic terms.

To understand what Big O notation is, we can take a look at a typical example, O(n²), which is usually pronounced “Big O squared”. The letter “n” here represents the input size, and the function “g(n) = n²” inside the “O()” gives us an idea of how complex the algorithm is with respect to the input size.

![](bigo.png)

1. O(n) - Linear Time

```javascript
const names = ['johnny cage', 'scorpion', 'sub-zero', 'raiden', 'shao tsung'];

const findScorpion = (array) => {
    for (let i = 0; i < array.length; i++) {
        if (array[i] === 'sub-zero') {
            console.log('Get Over Here!')
        }
    }
}
// this function has a big-O notation of O(n) --> Linear Time 

//In the function above, as the number of inputs increases, the number of operations increases linearly --> so in this function n = 5
findScorpion(names);
```

2. O(1) - Constant Time

```javascript
function compressFirstBox(boxes) {
    console.log(boxes[0]);
}
//this function operates only on the first box, so no matter how many inputs the array has, it will only operate once

function compressFirstTwoBoxes(boxes) {
    console.log([boxes[0]]);
    console.log(boxes[1]);
}
```