## Regular Expressions

Regular expressions are used in programming languages to match parts of strings. You create patterns to help you do that matching. 

If you want to find the word `"the"` in the string `"The dog chased the cat"`, you could use the following regular expression: `/the/`. Notice that quote marks are not required within the regular expression.

* Using the test method

```javascript
let myString = "Hello, World!";
let myRegex = /Hello/;
let result = myRegex.test(myString);
```

 You can search for multiple patterns using the `alternation`or OR operator: `|`.

 ```javascript
let petString = "James has a pet cat.";
let petRegex = /change|dog|cat|bird|fish/; // Change this line
let result = petRegex.test(petString);
 ```