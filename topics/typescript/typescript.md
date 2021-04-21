## TypeScript 

TypeScript is a typed superset of JavaScript that compiles to plain JavaScript. It offers classes, modules, and interfaces to help you build robust components.

* Alternative to JavaScript (superset - which basically means that it extends the abilities of JavaScript)

* Allows us to use strict types

* Supports modern features(arrow funcs, let, const)

* Needs to be compiled into JS code

* Extra features like: generics, interfaces, tuples etc.

---

### Compiling TypeScript

To be able to compile, install typescript first as shown below.

```bash
npm install -g typescript
```

Make sure you are in the desired directory, and have a .ts file and a .js file (preferably with the same name)

```bash
tsc filename.ts filename.js
```

In order not to keep compiling the code, run the following command:

```bash
tsc filename.ts -w
```

---

### Type Basics

```javascript
let name = 'john';
let age = 30;
let isWorking = false;

name = 10; //this will give you an error in TS because it was initially defined as a type string

name = 'sam'; // this will work just fine, same with age if you change it to another number of isWorking to true
```javascript

```javascript
const circ = (diameter: number) => {
    //here we calculate the circumference of a circle by multiplying the diameter with the 3.14(PI)
    //we define the type of the variable like this --> x: number, y: string
    //In JS, if we add a string as an argument to this function, it will give us NaN
    //In TS, this immediately warns us that something is wrong, it won't compile
    return diameter * Math.PI;
}

console.log(circ(5))
```

---

### Objects & Arrays

```javascript
let names = ["luigi", "mario", "yoshi"];

names.push("tod"); //this obviously works
names.push(3); //this gives us an error
```

```javascript
let mixed = ["john", 3, true, null];
mixed.push("hans"); // this works since mixed was initialized as an array with different data types
```

```javascript
let warrior = {
    name: "sub-zero",
    ability: "cryomancer",
    age: 30
}

warrior.name = "scorpion" // this is fine
warrior.ability = true // this is NOT fine, the data types of the properties of the object are defined when the object is initialized 

warrior.isAlive = false; // you can't add new properties once the object is declared
```

```javascript
let person = {
    name: "John",
    age: 30,
    isAlive: true
}

//this will not work because the property isAlive is left out, it has to be included in TS
person = {
    name: "Carol",
    age: 21
}
```

---

### Explicit Types

```javascript
//Explicitly defining types
let character: string = "John";
let age: number = 30;
let isLoggedIn: boolean = false;

let people: string[] = []; //or let people: string[]; --> this way, you won't be able to push items into the array, first you will need to initialize it like so --> people = [arrItems]
```

#### Union Types

Occasionally, you’ll run into a library that expects a parameter to be either a number or a string. We do this with adding union types.

```javascript
let mixed: (string | number)[] = [];

mixed.push('hello'); // this is ok
mixed.push(20); // this is ok
mixed.push(false); // this is NOT ok

//-----------------------------------
let strOrNum: string | number;

strOrNum = "hello"; // this is ok
strOrNum = 3; // this is ok
strOrNum = true; // this is NOT ok
```

```javascript
//Objects
let user: object;
user = {name: 'Hank', age: 20};
user = []; // this works because an array is also an object

let user2: {
    name: string,
    age: number,
    isLoggedIn: boolean
}
```

---