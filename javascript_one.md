Absolutely — here is a **complete JavaScript guide on Variables and Types** from an **interview + corporate + internship report** point of view.

---

# Variables and Types in JavaScript

JavaScript has two big parts here:

1. **Variables** — how data is stored and accessed
2. **Types** — what kind of data is stored

These two are very important because interviewers often test:

* `var` vs `let` vs `const`
* primitive vs non-primitive
* type conversion
* type checking
* scope and hoisting
* reference behavior

---

# 1. Variables

A variable is a container used to store data.

```js
let name = "Krishna";
```

Here:

* `let` is the variable keyword
* `name` is the variable name
* `"Krishna"` is the value

---

## A. `var`

`var` is the old way of declaring variables in JavaScript.

```js
var age = 20;
```

### Features of `var`

* function scoped
* can be re-declared
* can be updated
* hoisted with `undefined`

### Example

```js
console.log(a);
var a = 10;
```

Output:

```js
undefined
```

This happens because `var` is hoisted.

Internally, JavaScript treats it like:

```js
var a;
console.log(a);
a = 10;
```

---

## B. `let`

`let` is the modern way to declare variables.

```js
let age = 20;
```

### Features of `let`

* block scoped
* can be updated
* cannot be re-declared in the same scope
* hoisted but not initialized

### Example

```js
let x = 5;
x = 10;
console.log(x);
```

Output:

```js
10
```

But this is not allowed:

```js
let x = 5;
let x = 10;
```

This gives an error because redeclaration is not allowed.

---

## C. `const`

`const` is used for constants.

```js
const pi = 3.14;
```

### Features of `const`

* block scoped
* cannot be reassigned
* must be initialized at declaration
* hoisted but not initialized

### Example

```js
const a = 10;
a = 20;
```

This gives an error.

### Important point

`const` does **not** mean the value can never change in all cases. It means the **binding** cannot change.

Example:

```js
const user = {
  name: "Krishna"
};

user.name = "Aman";
console.log(user);
```

This works because the object itself is still mutable.

---

# 2. `var` vs `let` vs `const`

| Feature       | var      | let                    | const                     |
| ------------- | -------- | ---------------------- | ------------------------- |
| Scope         | Function | Block                  | Block                     |
| Re-declare    | Yes      | No                     | No                        |
| Reassign      | Yes      | Yes                    | No                        |
| Hoisted       | Yes      | Yes, but TDZ           | Yes, but TDZ              |
| Best practice | Avoid    | Use when value changes | Use when value stays same |

---

# 3. Scope of Variables

Scope means where a variable can be accessed.

## A. Global Scope

Declared outside any function or block.

```js
let name = "Krishna";

function show() {
  console.log(name);
}
```

`name` can be accessed inside the function because it is global.

---

## B. Function Scope

Variables declared inside a function are available only inside that function.

```js
function test() {
  let age = 20;
  console.log(age);
}

test();
console.log(age);
```

The last line gives an error.

---

## C. Block Scope

Variables declared with `let` and `const` inside `{}` are block scoped.

```js
if (true) {
  let a = 10;
  const b = 20;
}

console.log(a);
console.log(b);
```

Both give errors.

---

# 4. Outer Variable Reference

This is the part interviewers often ask in scope and closure topics.

An inner function can access a variable from its outer function.

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

```js
1
2
```

### Why?

Because `inner()` remembers the outer variable `count`.

This is called **lexical scope**.

---

## Lexical Scope

Lexical scope means:

> A function can access variables from the scope where it was defined, not where it is called.

Example:

```js
let name = "Global";

function outer() {
  let age = 20;

  function inner() {
    console.log(name);
    console.log(age);
  }

  inner();
}

outer();
```

`inner()` can access both `name` and `age`.

This is the base idea behind **closures**.

---

# 5. Hoisting

Hoisting means declarations are moved to the top of their scope during execution.

---

## `var` hoisting

```js
console.log(a);
var a = 10;
```

Output:

```js
undefined
```

Because `var a` is hoisted.

---

## `let` and `const` hoisting

```js
console.log(b);
let b = 10;
```

This gives an error.

This area is called the **Temporal Dead Zone (TDZ)**.

---

# 6. Temporal Dead Zone (TDZ)

The time between variable hoisting and actual initialization.

Example:

```js
console.log(x);
let x = 5;
```

Before `x` gets initialized, it exists in TDZ and cannot be accessed.

---

# 7. Data Types in JavaScript

JavaScript has two broad categories of types:

1. **Primitive types**
2. **Non-primitive types**

---

# 8. Primitive Data Types

Primitive values are simple, immutable values.

## A. String

```js
let name = "Krishna";
```

Used for text.

---

## B. Number

```js
let age = 20;
let price = 99.5;
```

Used for integers and decimals.

---

## C. BigInt

Used for very large integers.

```js
let bigNumber = 123456789012345678901234567890n;
```

---

## D. Boolean

```js
let isActive = true;
```

Only `true` or `false`.

---

## E. Undefined

A variable declared but not assigned.

```js
let x;
console.log(x);
```

Output:

```js
undefined
```

---

## F. Null

Represents intentional absence of value.

```js
let value = null;
```

Important interview point:

```js
typeof null
```

returns:

```js
"object"
```

This is a JavaScript bug-like historical behavior.

---

## G. Symbol

Used for unique identifiers.

```js
let id = Symbol("id");
```

---

# 9. Non-Primitive Data Types

These are reference types.

## A. Object

```js
let user = {
  name: "Krishna",
  age: 20
};
```

---

## B. Array

```js
let nums = [1, 2, 3];
```

Arrays are actually special objects.

---

## C. Function

Functions are also objects in JavaScript.

```js
function greet() {
  console.log("Hello");
}
```

---

# 10. `typeof`

Used to check the type of a value.

```js
typeof "hello"      // string
typeof 10           // number
typeof true         // boolean
typeof undefined    // undefined
typeof {}           // object
typeof []           // object
typeof function(){} // function
typeof null         // object
```

### Important interview point

* `typeof []` is `"object"`
* `typeof null` is `"object"`

---

# 11. Checking Arrays Properly

Since `typeof []` is object, use:

```js
Array.isArray([1, 2, 3]);
```

Output:

```js
true
```

---

# 12. Mutable vs Immutable

## Primitive values are immutable

```js
let str = "hello";
str[0] = "H";
console.log(str);
```

Output:

```js
hello
```

Strings do not change in place.

---

## Objects and arrays are mutable

```js
let arr = [1, 2, 3];
arr[0] = 99;
console.log(arr);
```

Output:

```js
[99, 2, 3]
```

---

# 13. Reference vs Value

This is a very important interview topic.

---

## Primitive values are copied by value

```js
let a = 10;
let b = a;

b = 20;

console.log(a);
console.log(b);
```

Output:

```js
10
20
```

`a` and `b` are independent copies.

---

## Objects are copied by reference

```js
let user1 = { name: "Krishna" };
let user2 = user1;

user2.name = "Aman";

console.log(user1.name);
console.log(user2.name);
```

Output:

```js
Aman
Aman
```

Both point to the same object.

---

# 14. Pass by Value and Pass by Reference

Strictly speaking, JavaScript is **pass by value**.

But for objects, the value being passed is a **reference**.

Example:

```js
function change(obj) {
  obj.name = "Updated";
}

let user = { name: "Krishna" };
change(user);

console.log(user.name);
```

Output:

```js
Updated
```

Because the reference value was copied, and both variables point to the same object.

---

# 15. Type Conversion

JavaScript often converts types automatically.

---

## A. String to Number

```js
let a = "10";
let b = Number(a);

console.log(b);
console.log(typeof b);
```

Output:

```js
10
number
```

---

## B. Number to String

```js
let a = 20;
let b = String(a);

console.log(b);
console.log(typeof b);
```

---

## C. Boolean Conversion

```js
Boolean(1);      // true
Boolean(0);      // false
Boolean("");     // false
Boolean("Hi");   // true
```

---

# 16. Type Coercion

Automatic conversion done by JavaScript.

```js
console.log("5" + 1);
```

Output:

```js
51
```

Because number is converted to string.

But:

```js
console.log("5" - 1);
```

Output:

```js
4
```

Because `-` forces numeric conversion.

---

# 17. Equality Operators

## `==` loose equality

Compares after type conversion.

```js
console.log(5 == "5");
```

Output:

```js
true
```

---

## `===` strict equality

Compares value and type both.

```js
console.log(5 === "5");
```

Output:

```js
false
```

### Interview tip

Always prefer `===` unless you specifically need coercion.

---

# 18. Truthy and Falsy Values

JavaScript treats some values as false in conditions.

## Falsy values:

* `false`
* `0`
* `-0`
* `""`
* `null`
* `undefined`
* `NaN`
* `0n`

Everything else is truthy.

Example:

```js
if ("hello") {
  console.log("truthy");
}
```

This runs.

---

# 19. Special Values

## NaN

Means "Not a Number"

```js
console.log(Number("abc"));
```

Output:

```js
NaN
```

Check it using:

```js
isNaN(value)
```

---

## Infinity

```js
console.log(10 / 0);
```

Output:

```js
Infinity
```

---

# 20. Variable Naming Rules

Valid variable names:

* can contain letters, digits, underscore, dollar sign
* cannot start with a digit
* cannot use reserved keywords

Valid:

```js
let userName = "Krishna";
let _age = 20;
let $price = 100;
```

Invalid:

```js
let 1name = "abc";
let class = 10;
```

---

# 21. Best Practices for Variables

Use:

* `const` by default
* `let` when reassignment is needed
* avoid `var`

Example:

```js
const name = "Krishna";
let count = 0;
```

Good naming style:

* `camelCase`
* meaningful names
* avoid single-letter names unless in loops

---

# 22. Common Interview Questions

### 1. Difference between `var`, `let`, and `const`

### 2. What is hoisting?

### 3. What is TDZ?

### 4. Difference between primitive and non-primitive types

### 5. Why is `typeof null` `"object"`?

### 6. Why is `typeof []` `"object"`?

### 7. Difference between `==` and `===`

### 8. What is type coercion?

### 9. What is the difference between copy by value and copy by reference?

### 10. What are truthy and falsy values?

### 11. What is lexical scope?

### 12. How can an inner function access outer variables?

---

# 23. Simple Report-Ready Summary

You can write this in your internship report:

> Today I studied JavaScript variables and data types in detail. I learned the difference between `var`, `let`, and `const`, along with their scope, hoisting behavior, and practical usage. I also explored primitive and non-primitive data types, type conversion, type coercion, and comparison operators. One important concept I understood was lexical scope, where an inner function can access outer variables through the scope chain. I also revised truthy/falsy values, mutable vs immutable data, and reference behavior in objects and arrays.

---

# 24. Final Revision Order

Study in this order:

1. `var`, `let`, `const`
2. Scope
3. Hoisting and TDZ
4. Primitive vs non-primitive types
5. `typeof`
6. Type conversion and coercion
7. `==` vs `===`
8. Truthy/falsy
9. Reference vs value
10. Outer variable reference / lexical scope

---

If you need a next step, I can turn this into a **proper internship report format** with headings like **What I Learned, Key Findings, Practical Examples, and Conclusion**.
