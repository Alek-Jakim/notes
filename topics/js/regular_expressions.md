# Regular Expressions

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
--- 

### Ignore case while matching

* Use the `i` flag to ignore case

```javascript
let myString = "SoMeThingWithDifferentCassing";
let fccRegex = /SoMeThingWithDifferentCassing/i; // Change this line
let result = fccRegex.test(myString);

console.log(result)
```
---

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
---

### Find More Than the First Match

To search or extract a pattern more than once, you can use the `g` flag.

```javascript
let twinkleStar = "Twinkle, twinkle, little star";
let starRegex = /twinkle/gi; // Change this line
let result = twinkleStar.match(starRegex); // Change this line

console.log(result) //Output: ['Twinkle', 'twinkle']
```
---

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

---

### Match Single Character with Multiple Possibilities

You can search for a literal pattern with some flexibility with character classes. Character classes allow you to define a group of characters you wish to match by placing them inside square (`[` and `]`) brackets.

For example, you want to match `bag`, `big`, and `bug` but not `bog`. You can create the regex `/b[aiu]g/` to do this. The `[aiu]` is the character class that will only match the characters a, i, or u.

```javascript
let quoteSample = "Beware of bugs in the above code; I have only proved it correct, not tried it.";
let vowelRegex = /[aeiou]/gi; 
let result = quoteSample.match(vowelRegex);

//Here I used the character class with vowels (a, e, i, o, u) in the regex vowelRegex to find all the vowels in the string quoteSample.

// I made sure to match both upper- and lowercase vowels.
```
---

### Match Letters of the Alphabet

Inside a character set, you can define a range of characters to match using a hyphen character: `-`.

For example, to match lowercase letters a through e you would use `[a-e]`.

```javascript
let quoteSample = "The quick brown fox jumps over the lazy dog.";
let alphabetRegex = /[a-z]/gi; 
let result = quoteSample.match(alphabetRegex); 

//Here I match all the letters in the string quoteSample.
```
---

### Match Numbers and Letters of the Alphabet

Using the hyphen (-) to match a range of characters is not limited to letters. It also works to match a range of numbers.

For example, `/[0-5]/` matches any number between 0 and 5, including the 0 and 5.

```javascript
let jennyStr = "Jenny8675309";
let myRegex = /[a-z0-9]/ig;
jennyStr.match(myRegex);
```
---

### Match Single Characters Not Specified

You could also create a set of characters that you do not want to match. These types of character sets are called **negated character sets**.

To create a negated character set, you place a caret character (`^`) after the opening bracket and before the characters you do not want to match.

For example, `/[^aeiou]/gi` matches all characters that are not a vowel. Note that characters like `.`, `!`, `[`, `@`, `/` and white space are matched - the negated vowel character set only excludes the vowel characters.



```javascript
let quoteSample = "3 blind mice.";
let myRegex = /[^aeiou0-9]/gi; // Change this line
let result = quoteSample.match(myRegex); // Change this line

//Here I created a single regex that matches all characters that are not a number or a vowel
```

---

### Match Characters that Occur One or More Times

Sometimes, you need to match a character (or group of characters) that appears one or more times in a row. This means it occurs at least once, and may be repeated.

You can use the `+` character to check if that is the case. Remember, the character or pattern has to be present consecutively. That is, the character has to repeat one after the other.

For example, `/a+/g` would find one match in abc and return `["a"]`. Because of the +, it would also find a single match in aabc and return `["aa"]`.

```javascript
let difficultSpelling = "Mississippi";
let myRegex = /s+/gi; 
let result = difficultSpelling.match(myRegex);

// Here I find  matches when the letter s occurs one or more times in Mississippi.
```

---

### Match Characters that Occur Zero or More Times

There's also an option that matches characters that occur zero or more times. The character to do this is the asterisk or star: `*`.

```javascript
let chewieQuote = 'Aaaaaaaaaaaaaaaarrrgh!'
let chewieRegex = /Aa*/
let result = chewieQuote.match(chewieRegex);

console.log(result) // Output: Aaaaaaaaaaaaaaaa
```
---

### Find Characters with Lazy Matching

* **Greedy match** - finds the longest possible part of a string that fits the regex pattern and returns it as a match

* **Lazy match** - finds the smallest possible part of the string that satisfies the regex pattern

You can apply the regex `/t[a-z]*i/` to the string `"titanic"`. Regular expressions are by default greedy, so the match would return `["titani"]`. It finds the largest sub-string possible to fit the pattern.

However, you can use the `?` character to change it to lazy matching. `"titanic"` matched against the adjusted regex of `/t[a-z]*?i/` returns `["ti"]`.

**Note**: Parsing HTML with regular expressions should be avoided, but pattern matching an HTML string with regular expressions is completely fine.

```javascript
let text = "<h1>Winter is coming</h1>";
let myRegex = /<.*?>/; 
let result = text.match(myRegex);

console.log(result) // <h1>
```