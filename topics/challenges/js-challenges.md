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
