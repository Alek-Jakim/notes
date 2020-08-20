### Promise Chaining

To demonstrate promise chaining, the following function will be used to simulate an
asynchronous task. In reality, it’s just adding up a couple of numbers, waiting two seconds, and fulfilling the promise with the sum.

```javascript
const add = (a, b) => {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            if (a < 0 || b < 0) {
            return reject('Numbers must be non-negative')
        }
            resolve(a + b)
        }, 2000)
    })
}
```
With the dummy asynchronous function defined, promise chaining can be used to call add
twice. The code below adds up 1 and 2 for a total of 3. It then uses the sum of 3 as the
input for another call to add. The second call to add adds up 3 and 4 for a total of 7. 


Promise chaining occurs when the then callback function returns a promise. This allows
you to chain on another then call which will run when the second promise is fulfilled. catch can still be called to handle any errors that might occur along the way.

```javascript
add(1, 2).then((sum) => {
    console.log(sum) // Will print 3
    return add(sum, 4)
}).then((sum2) => {
    console.log(sum2) // Will print 7
}).catch((e) => {
    console.log(e)
})
```

```javascript
const mongoose = require('../src/db/mongoose');
const Task = require('../src/models/task');

Task.findByIdAndDelete('5f3b7df885346d0ce073df7e')
    .then((res) => {
        console.log(res);
        return Task.countDocuments({ completed: true })
    })
    .then((res) => {
        console.log(res)
    })
    .catch((e) => {
        console.log(e);
    })
```


### Async/Await

```javascript
const doWork = async () => {
    const sum = await add(1, 99)
    const sum2 = await add(sum, 50)
    const sum3 = await add(sum2, 3)
    return sum3
}
doWork().then((result) => {
    console.log('result', result)
}).catch((e) => {
    console.log('e', e)
})
```

It’s important to note that async and await are syntax enhancements for working with
promises. Promises are still at the core of asynchronous code that uses async and await.