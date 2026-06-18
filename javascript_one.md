Since you want something you can **study from and later turn into an internship report**, I'll focus on the concepts that are actually useful in interviews and real projects, not just theory.

# 1. Function Declaration vs Function Expression

## Function Declaration

```js
function greet() {
    console.log("Hello");
}
```

### Characteristics

* Hoisted completely.
* Can be called before definition.

```js
sayHello();

function sayHello() {
    console.log("Hello");
}
```

Output:

```text
Hello
```

---

## Function Expression

```js
const greet = function() {
    console.log("Hello");
};
```

### Characteristics

* Stored inside a variable.
* Not fully hoisted.

```js
greet();

const greet = function() {
    console.log("Hello");
};
```

Output:

```text
ReferenceError
```

---

# 2. Arrow Functions

ES6 introduced shorter syntax.

Traditional:

```js
function add(a, b) {
    return a + b;
}
```

Arrow:

```js
const add = (a, b) => {
    return a + b;
};
```

Short form:

```js
const add = (a, b) => a + b;
```

---

## Important Interview Question

### Arrow Functions don't have their own `this`

Normal Function:

```js
const user = {
    name: "Krishna",
    greet: function() {
        console.log(this.name);
    }
};

user.greet();
```

Output:

```text
Krishna
```

Arrow Function:

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

Because arrow functions inherit `this` from surrounding scope.

---

# 3. Parameters vs Arguments

Function definition:

```js
function add(a, b) {
    return a + b;
}
```

### Parameters

```js
a, b
```

are parameters.

### Arguments

```js
add(10, 20);
```

10 and 20 are arguments.

---

# 4. Default Parameters

```js
function greet(name = "Guest") {
    console.log(name);
}
```

```js
greet();
```

Output:

```text
Guest
```

---

# 5. Rest Parameters

Collects multiple values.

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

# 6. Spread Operator

Expands arrays or objects.

```js
const arr1 = [1,2,3];

const arr2 = [...arr1];
```

Result:

```js
[1,2,3]
```

Merge arrays:

```js
const a = [1,2];
const b = [3,4];

const result = [...a, ...b];
```

Output:

```js
[1,2,3,4]
```

---

# 7. Scope

A variable's accessibility area.

## Global Scope

```js
let name = "Krishna";

function show() {
    console.log(name);
}
```

Accessible everywhere.

---

## Function Scope

```js
function test() {
    let age = 20;
}

console.log(age);
```

Output:

```text
ReferenceError
```

---

## Block Scope

```js
if(true){
    let x = 10;
}

console.log(x);
```

Output:

```text
ReferenceError
```

---

# 8. Lexical Scope

The most important topic before closures.

A function can access variables from its parent scope.

```js
let globalVar = "Global";

function outer() {

    let outerVar = "Outer";

    function inner() {
        console.log(globalVar);
        console.log(outerVar);
    }

    inner();
}

outer();
```

Output:

```text
Global
Outer
```

---

# OUTER VARIABLE REFERENCE PART (VERY IMPORTANT)

This is what interviewers mean by:

> "How can inner function access outer variables?"

Consider:

```js
function outer() {

    let count = 0;

    function inner() {
        count++;
        console.log(count);
    }

    inner();
    inner();
}

outer();
```

Output:

```text
1
2
```

### Why?

When JavaScript creates `inner()`, it remembers:

```js
count
```

from the outer scope.

This remembered connection is called a:

# Closure

---

# 9. Closures

A closure happens when:

> A function remembers variables from its outer scope even after the outer function has finished execution.

Example:

```js
function outer() {

    let count = 0;

    return function() {
        count++;
        return count;
    };
}

const counter = outer();

console.log(counter());
console.log(counter());
console.log(counter());
```

Output:

```text
1
2
3
```

---

## What Happens Internally?

Step 1:

```js
const counter = outer();
```

Creates:

```js
count = 0
```

Step 2:

```js
outer() finishes
```

Normally variables die.

BUT:

Returned function still references:

```js
count
```

So JS keeps it alive.

This is Closure.

---

## Real World Use

### Private Variables

```js
function createBankAccount() {

    let balance = 1000;

    return {
        deposit(amount) {
            balance += amount;
        },

        getBalance() {
            return balance;
        }
    };
}
```

Usage:

```js
const account = createBankAccount();

account.deposit(500);

console.log(account.getBalance());
```

Output:

```text
1500
```

Nobody can directly access:

```js
balance
```

This is data hiding.

---

# 10. Callback Functions

A function passed into another function.

```js
function greet(callback) {

    console.log("Hello");

    callback();
}

function bye() {
    console.log("Bye");
}

greet(bye);
```

Output:

```text
Hello
Bye
```

---

# 11. Higher Order Functions

A function that:

* Receives another function
  OR
* Returns another function

Example:

```js
function operate(fn, a, b) {
    return fn(a, b);
}
```

Usage:

```js
function add(a, b) {
    return a + b;
}

console.log(operate(add, 10, 20));
```

---

# 12. map()

Transforms every element.

```js
const nums = [1,2,3];

const result = nums.map(num => num * 2);
```

Output:

```js
[2,4,6]
```

---

# 13. filter()

Filters elements.

```js
const nums = [1,2,3,4,5];

const even = nums.filter(num => num % 2 === 0);
```

Output:

```js
[2,4]
```

---

# 14. reduce()

Reduces array to one value.

```js
const nums = [1,2,3,4];

const total = nums.reduce((acc, curr) => {
    return acc + curr;
}, 0);
```

Output:

```text
10
```

---

# 15. Hoisting

JavaScript moves declarations to the top.

Works:

```js
hello();

function hello() {
    console.log("Hi");
}
```

Doesn't work:

```js
hello();

const hello = function() {
    console.log("Hi");
};
```

---

# 16. call(), apply(), bind()

Used to manually set `this`.

### call()

```js
function greet(city) {
    console.log(this.name, city);
}

const user = {
    name: "Krishna"
};

greet.call(user, "Delhi");
```

Output:

```text
Krishna Delhi
```

---

### apply()

Arguments passed as array.

```js
greet.apply(user, ["Delhi"]);
```

---

### bind()

Returns a new function.

```js
const newFunc = greet.bind(user);

newFunc("Delhi");
```

---

# 17. Pure Functions

Always same input → same output.

```js
function add(a, b) {
    return a + b;
}
```

Pure.

---

# 18. Impure Functions

Depend on external state.

```js
let tax = 10;

function calculate(price) {
    return price + tax;
}
```

Impure.

---

# 19. Recursion

Function calling itself.

```js
function factorial(n) {

    if(n === 1)
        return 1;

    return n * factorial(n - 1);
}
```

```js
factorial(5);
```

Output:

```text
120
```

---

# Interview Revision Sheet (Most Important)

Prepare these thoroughly:

✅ Function Declaration vs Expression
✅ Arrow Functions
✅ Parameters, Arguments, Rest, Spread
✅ Scope
✅ Lexical Scope
✅ Closures ⭐⭐⭐
✅ Callback Functions
✅ Higher Order Functions ⭐⭐⭐
✅ map, filter, reduce ⭐⭐⭐
✅ Hoisting ⭐⭐⭐
✅ this Keyword ⭐⭐⭐
✅ call, apply, bind ⭐⭐⭐
✅ Pure vs Impure Functions
✅ Recursion

For your internship report, the strongest "new learning" section would be **Lexical Scope, Closures, Higher-Order Functions, and call/apply/bind**, because those are the topics that go beyond basic ES6 syntax and demonstrate deeper understanding of JavaScript functions.
