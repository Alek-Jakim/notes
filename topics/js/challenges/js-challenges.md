## JS Challenges

1. FizzBuzz

```javascript
for (let i = 0; i <= 100; i++) {
    i % 3 === 0 && i % 5 === 0 ? console.log('FizzBuzz') : i % 3 === 0 ? console.log('Fizz') : i % 5 === 0 ? console.log('Buzz') : console.log(i);
}
//Probably better with if else statements
```

2. Reverse String

```javascript
const reverseString = str => str.split('').reverse().join('');
```

3. Check if the string is a palindrome

```javascript
const isPalindrome = (str) => {
    let revString = str.split('').reverse().join('').toLowerCase();
    return str.toLowerCase() === revString ? true : false;
}
```

4. Reverse Integer

```javascript
//Remember - the parseFloat() function parses an argument (converting it to a string first if needed) and returns a floating point number.

const reverseInteger = num => parseFloat(num.toString().split('').reverse().join('')) * Math.sign(num);

//The Math.sign() function returns either a positive or negative +/- 1, indicating the sign of a number passed into the argument. If the number passed into Math.sign() is 0, it will return a +/- 0. Note that if the number is positive, an explicit (+) will not be returned.

```

5. Capitalize Letters

```javascript
const capitalizeLetters = (str) => {
    //First create an array
    const strArr = str.toLowerCase().split(' ');

    //Now loop through the array
    for (let i = 0; i < strArr.length; i++) {
        strArr[i] = strArr[i].substring(0, 1).toUpperCase() + strArr[i].substring(1);
    }
    //Return the value, but not before joining it; otherwise it will give you an array
    return strArr.join(' ');
}
```

6. maxChar 

```javascript
//Check for the most common character in a string
const maxCharacter = (str) => {
    let charMap = {};
    let maxNum = 0;
    let maxChar = '';

    str.split('').forEach((char) => {
        if (charMap[char]) {
            charMap[char]++
        } else {
            charMap[char] = 1
        }
    })

    for (let char in charMap) {
        if (charMap[char] > maxNum) {
            maxNum = charMap[char];
            maxChar = char;
        }
    }

    return maxChar;
}
```

7. Create a grade calculator

```javascript
//Create a grade calculator

const calculateGrades = (score, totalScore) => {
    let percent = (score / totalScore) * 100;

    return percent >= 90 ? 'You got an A'
        : percent >= 75 ? 'You got a B'
            : percent >= 50 ? 'You got a C'
                : percent >= 30 ? 'You got a D'
                    : percent < 29 ? 'You got an F'
                        : 'Please check your input!'
}
```

8. Create an Expense Tracker
```javascript
let myAccount = {
    name: 'Alek',
    expenses: 0,
    income: 0
}
const addIncome = (account, amount) => {
    return account.income += amount;
}
const addExpense = (account, amount) => {
    return account.expenses += amount;
}
const accountBalance = (account) => {
    return `Your account balance is $${account.income - account.expenses}.`
}
```

9. Replace every char in a string with the following char in the alphabet

```javascript
const moveCharForward = (str) => {
    return str
        .split('')
        .map(char => String.fromCharCode(char.charCodeAt(0) + 1))
        .join('')
}
```

10. Get the current date dd--mm--yyyy

```javascript
const getCurrDate = () => {
    const date = new Date();
    return `Today's date is ${date.getDate()}-${date.getMonth() + 1}-${date.getFullYear()}`
}
```

11. Create a string adding 'New' if the str doesn't already start with New

```javascript
const novelString = str => str.toLowerCase().includes('new') ? str : 'new ' + str;
```


12. Use Recursion to Create a Countdown

```javascript
function countdown(n){
  if(n < 1) {
    return [];
  } else {
    let countArr = countdown(n - 1)
    countArr.push(n)
    countArr.sort((a, b) => {
      return b - a
    })
    return countArr
  }
}
```

13. Use Recursion to Create a Range of Numbers

```javascript
function rangeOfNumbers(startNum, endNum) {
  if(endNum - startNum === 0){
    return [startNum];
  } else {
    let myArr = rangeOfNumbers(startNum, endNum - 1)
    myArr.push(endNum)
    return myArr
  }
};
```
14. Factorialize a number

```javascript
const factorialize = (num) => num === 0 ? 1 : num * factorialize(num - 1);
//The factorial of a positive integer n, denoted by n!, is the product of all positive integers less than or equal to n

//for example 5! = 1 * 2 * 3 * 4 * 5 = 120
```

15. Return Largest Numbers in Arrays

* Create a variable to store the results as an array.
* Create an outer loop to iterate through the outer array.
* Create a second variable to hold the largest number and initialise it with the first number. This must be outside an inner loop so it won’t be reassigned until we find a larger number.
* Create said inner loop to work with the sub-arrays.
* Check if the element of the sub array is larger than the currently stored largest number. If so, then update the number in the variable.
* After the inner loop, save the largest number in the corresponding position inside of the results array.
* And finally return said array.

```javascript
function largestOfFour(arr) {
  let results = [];
  for(let i = 0; i <arr.length; i++){
    let largestNum = arr[i][0]
    for(let y = 1; y < arr[i].length; y++) {
      if(arr[i][y] > largestNum){
        largestNum = arr[i][y]
      }
    }
    results[i] = largestNum
  }
  return results;
}
```

16. Check if a string (first argument, str) ends with the given target string (second argument, target).

First we use the slice method copy the string.
In order to get the last characters in str equivalent to the target's length we use the slice method.
The first parameter inside the slice method is the starting index and the second parameter would be the ending index.
For example str.slice(10, 17) would return give me.
In this case we only include one parameter which it will copy everything from the starting index.
We substract the length of str and the length of target, that way, we shall get the last remaining characters equivalent to the target's length.
Finally we compare the return result of slice to target and check if they have the same characters.

```javascript
const confirmEnding = (str, ending) => str.slice(str.length - ending.length) === ending
```

17. Repeat a string

```javascript
function repeatStringNumTimes(str, num) {
  if(num <= 0){
    return ''
  }
  let newStr = str
  for(let i = 1; i < num; i++) {
    newStr =str + newStr
  }
  return newStr;
}
```

18. Truncate a string if it is longer than the given maximum string length

```javascript
const truncateString = (str, num) => str.length > num ? str.slice(0, num) + '...' : str;
```

19. Create a function that looks through an array arr and returns the first element in it that passes a 'truth test'. This means that given an element x, the 'truth test' is passed if func(x) is true. If no element passes the test, return undefined.

```javascript
const findElement = (arr, func) => arr.find(func)
```


20. Check if a value is classified as a boolean primitive. Return true or false.

```javascript
const booWho = (bool) => typeof bool === 'boolean' ? true : false
```