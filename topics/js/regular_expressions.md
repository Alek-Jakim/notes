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

### Ignore case while matching

* Use the `i` flag to ignore case

```javascript
let myString = "SoMeThingWithDifferentCassing";
let fccRegex = /SoMeThingWithDifferentCassing/i; // Change this line
let result = fccRegex.test(myString);

console.log(result)
```

### Extract Matches

The `match()` method retrieves the result of matching a string against a regular expression. You can also extract the actual matches you found with the `.match()` method.

```javascript
let extractStr = "Extract the word 'coding' from this string.";
let codingRegex = /coding/; // Change this line
let result = extractStr.match(codingRegex); // Change this line

console.log(result) 
/*Output:
[ 'coding',
  index: 18,
  input: 'Extract the word \'coding\' from this string.',
  groups: undefined ]

*/
```

### Find More Than the First Match

To search or extract a pattern more than once, you can use the `g` flag.

```javascript
let twinkleStar = "Twinkle, twinkle, little star";
let starRegex = /twinkle/gi; // Change this line
let result = twinkleStar.match(starRegex); // Change this line

console.log(result) //Output: ['Twinkle', 'twinkle']
```

### Match Anything with Wildcard Period

The wildcard character `.` will match any one character. You can use the wildcard character just like any other character in the regex.  For example, if you wanted to match hug, huh, hut, and hum, you can use the regex `/hu./` to match all four words.

```javascript
let humStr = "I'll hum a song";
let hugStr = "Bear hug";
let huRegex = /hu./;
huRegex.test(humStr);
huRegex.test(hugStr);
```

Both of these `test` calls would return `true`.
