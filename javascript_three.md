# Modern JavaScript (ES6+) Complete Guide

---

# 1. What is ES6?

ES6 (ECMAScript 2015) introduced major improvements to JavaScript.

Common ES6 features:

* let
* const
* Arrow Functions
* Template Literals
* Destructuring
* Spread Operator
* Rest Parameters
* Default Parameters
* Enhanced Object Literals
* Classes
* Modules
* Promises
* for...of Loop
* Map
* Set

---

# 2. let and const

## let

Block scoped variable.

```js
let age = 20;

if(true){
    let age = 25;
    console.log(age);
}

console.log(age);
```

Output:

```text
25
20
```

---

## const

Cannot be reassigned.

```js
const PI = 3.14;
```

Invalid:

```js
const PI = 3.14;
PI = 10;
```

---

# 3. Arrow Functions

## Traditional Function

```js
function add(a, b) {
    return a + b;
}
```

---

## Arrow Function

```js
const add = (a, b) => {
    return a + b;
};
```

---

## Single Parameter

```js
const square = num => {
    return num * num;
};
```

---

## Implicit Return

```js
const square = num => num * num;
```

---

## Returning Objects

Wrong:

```js
const createUser = () => {
    name: "Krishna";
};
```

Correct:

```js
const createUser = () => ({
    name: "Krishna"
});
```

---

# 4. Arrow Function vs Normal Function

## this Keyword

Normal Function

```js
const user = {
    name: "Krishna",

    greet() {
        console.log(this.name);
    }
};

user.greet();
```

Output:

```text
Krishna
```

---

Arrow Function

```js
const user = {
    name: "Krishna",

    greet: () => {
        console.log(this.name);
    }
};

user.greet();
```

Output:

```text
undefined
```

Arrow functions do not create their own `this`.

---

## arguments Object

Normal Function

```js
function test() {
    console.log(arguments);
}

test(1,2,3);
```

Works.

---

Arrow Function

```js
const test = () => {
    console.log(arguments);
};
```

Error.

Arrow functions do not have `arguments`.

---

## Constructor Usage

Normal Function

```js
function User(name) {
    this.name = name;
}

const u = new User("Krishna");
```

Works.

---

Arrow Function

```js
const User = (name) => {
    this.name = name;
};

new User("Krishna");
```

Error.

Arrow functions cannot be constructors.

---

# 5. Default Parameters

Before ES6

```js
function greet(name) {
    name = name || "Guest";
    return name;
}
```

---

ES6

```js
function greet(name = "Guest") {
    return name;
}
```

---

Multiple Defaults

```js
function createUser(
    name = "Guest",
    age = 18
){
    console.log(name, age);
}
```

---

# 6. Template Literals

Before ES6

```js
const name = "Krishna";

console.log("Hello " + name);
```

---

ES6

```js
const name = "Krishna";

console.log(`Hello ${name}`);
```

---

Multiple Variables

```js
const first = "Krishna";
const last = "Aggarwal";

console.log(`${first} ${last}`);
```

---

Multi-Line Strings

```js
const text = `
Hello
World
`;
```

---

Expression Evaluation

```js
const a = 10;
const b = 20;

console.log(`${a + b}`);
```

Output:

```text
30
```

---

# 7. Destructuring

Extract values from arrays or objects.

---

# Array Destructuring

```js
const colors = [
    "red",
    "green",
    "blue"
];

const [a, b, c] = colors;

console.log(a);
```

Output:

```text
red
```

---

## Skip Values

```js
const colors = [
    "red",
    "green",
    "blue"
];

const [first, , third] = colors;
```

---

## Default Values

```js
const [a = "default"] = [];
```

Output:

```text
default
```

---

## Swapping Variables

Before ES6

```js
let a = 10;
let b = 20;

let temp = a;
a = b;
b = temp;
```

---

ES6

```js
let a = 10;
let b = 20;

[a, b] = [b, a];
```

---

# Object Destructuring

```js
const user = {
    name: "Krishna",
    age: 20
};

const { name, age } = user;

console.log(name);
```

Output:

```text
Krishna
```

---

## Rename Variables

```js
const user = {
    name: "Krishna"
};

const {
    name: userName
} = user;

console.log(userName);
```

---

## Default Values

```js
const user = {
    name: "Krishna"
};

const {
    city = "Delhi"
} = user;
```

Output:

```text
Delhi
```

---

## Nested Object Destructuring

```js
const user = {
    name: "Krishna",

    address: {
        city: "Delhi",
        state: "Delhi"
    }
};

const {
    address: {
        city
    }
} = user;

console.log(city);
```

---

## Function Parameter Destructuring

```js
const user = {
    name: "Krishna",
    age: 20
};

function display({
    name,
    age
}) {
    console.log(name, age);
}

display(user);
```

---

# 8. Spread Operator (...)

Expands iterable values.

---

## Arrays

```js
const arr1 = [1,2,3];

const arr2 = [...arr1];
```

Result:

```js
[1,2,3]
```

---

## Merge Arrays

```js
const a = [1,2];
const b = [3,4];

const result = [
    ...a,
    ...b
];
```

Result:

```js
[1,2,3,4]
```

---

## Objects

```js
const user = {
    name: "Krishna"
};

const updated = {
    ...user,
    age: 20
};
```

Result:

```js
{
    name: "Krishna",
    age: 20
}
```

---

## Copying Objects

```js
const copy = {
    ...user
};
```

---

# 9. Rest Parameters (...)

Collect multiple values.

```js
function sum(...numbers) {
    console.log(numbers);
}
```

```js
sum(1,2,3,4);
```

Output:

```js
[1,2,3,4]
```

---

## Difference Between Rest and Spread

Rest:

```js
function test(...args) {}
```

Collects values.

---

Spread:

```js
const arr = [1,2,3];

console.log(...arr);
```

Expands values.

---

# 10. Enhanced Object Literals

Before ES6

```js
const name = "Krishna";

const user = {
    name: name
};
```

---

ES6

```js
const name = "Krishna";

const user = {
    name
};
```

---

## Method Shorthand

Before ES6

```js
const user = {
    greet: function() {
        console.log("Hello");
    }
};
```

---

ES6

```js
const user = {
    greet() {
        console.log("Hello");
    }
};
```

---

# 11. for...of Loop

Iterates over iterable values.

```js
const nums = [1,2,3];

for(const num of nums){
    console.log(num);
}
```

Output:

```text
1
2
3
```

---

# 12. Map

Stores key-value pairs.

```js
const map = new Map();

map.set("name", "Krishna");

console.log(
    map.get("name")
);
```

Output:

```text
Krishna
```

---

# 13. Set

Stores unique values.

```js
const set = new Set();

set.add(1);
set.add(1);
set.add(2);

console.log(set);
```

Result:

```text
Set(2) {1,2}
```

---

# 14. Modules

Export

```js
export const name = "Krishna";
```

---

Import

```js
import { name } from "./user.js";
```

---

Default Export

```js
export default function greet() {}
```

Import

```js
import greet from "./user.js";
```

---

# 15. Promises

Represents a future result.

```js
const promise = new Promise(
    (resolve, reject) => {

        resolve("Success");
    }
);
```

---

Using Promise

```js
promise.then(result => {
    console.log(result);
});
```

---

# Interview Questions

### Arrow Functions

* Difference between arrow and normal functions
* this behavior
* arguments behavior
* Constructor support
* Implicit return

### Destructuring

* Array destructuring
* Object destructuring
* Nested destructuring
* Default values
* Renaming variables
* Function parameter destructuring

### Spread & Rest

* Difference between spread and rest
* Array merging
* Object copying
* Function arguments

### ES6 Features

* let vs const
* Template literals
* for...of
* Enhanced object literals
* Modules
* Promises
* Map
* Set

### Most Asked Topics

1. Arrow Functions
2. this in Arrow Functions
3. Destructuring
4. Spread vs Rest
5. Template Literals
6. let vs const
7. Modules
8. Promises
9. Map vs Object
10. Set and unique values
