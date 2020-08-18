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