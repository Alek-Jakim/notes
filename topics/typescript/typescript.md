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