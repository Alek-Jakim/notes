## Recursion

Recursion is when a function keeps calling itself until it doesn't have to anymore. The function keeps calling itself but with a smaller input every single time.

The function doesn't decide for itself when to stop. We tell it when to stop. We give the function a condition known as a **base case**.

* 1st example

```javascript
const count = n => {
    if (n === 0) {
        return;
    }
    console.log(n)
    return count(n - 1);
};
```

* 2nd Example

```javascript
const evenOrOdd = (n) => {
    if (n % 2 === 0) {
        return 'Even'
    } else if (n % 3 === 0) {
        return 'Odd'
    }
    return evenOrOdd(n - 2);
}
```


### Recursion vs Loops

When it comes to speed, a loop runs way faster than a recursive function. 

### Exercises

1. Write a program that reverses a string using recursion. Given the string "freeCodeCamp" your program should return "pmaCedoCeerf".

2. Write a program that returns the number of times a character appears in string. Your program should receive a string and the character. It should then return number of times the character appears in the string. Given the string "JavaScript" and a character "a", your program should return 2.