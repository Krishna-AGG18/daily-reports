If your topic is **"Arrays & Objects"**, then **map(), filter(), reduce() are only a small part of it**.

For internship preparation, assessments, and interviews, the complete Arrays & Objects section should look like this:

# ARRAYS

## 1. What is an Array?

Collection of ordered values stored in a single variable.

```js
const fruits = ["Apple", "Banana", "Mango"];
```

Characteristics:

* Indexed (starts from 0)
* Dynamic size
* Can store mixed data types

```js
const arr = [1, "Hello", true, null];
```

---

# 2. Creating Arrays

```js
const arr1 = [1,2,3];

const arr2 = new Array(1,2,3);
```

---

# 3. Accessing Elements

```js
const fruits = ["Apple", "Banana"];

console.log(fruits[0]);
```

Output:

```text
Apple
```

---

# 4. Updating Elements

```js
const arr = [1,2,3];

arr[0] = 100;
```

---

# 5. Array Length

```js
const arr = [1,2,3];

console.log(arr.length);
```

Output:

```text
3
```

---

# 6. Adding Elements

## push()

Adds at end.

```js
arr.push(4);
```

---

## unshift()

Adds at beginning.

```js
arr.unshift(0);
```

---

# 7. Removing Elements

## pop()

Removes last.

```js
arr.pop();
```

---

## shift()

Removes first.

```js
arr.shift();
```

---

# 8. Searching

## includes()

```js
arr.includes(2);
```

Returns boolean.

---

## indexOf()

```js
arr.indexOf(3);
```

Returns index.

---

## lastIndexOf()

```js
arr.lastIndexOf(3);
```

---

# 9. Iterating Arrays

## for Loop

```js
for(let i=0;i<arr.length;i++){
    console.log(arr[i]);
}
```

---

## for...of

```js
for(const item of arr){
    console.log(item);
}
```

---

## forEach()

```js
arr.forEach(item=>{
    console.log(item);
});
```

---

# 10. map()

Creates a new transformed array.

```js
const nums = [1,2,3];

const doubled = nums.map(
    num => num * 2
);
```

Output:

```js
[2,4,6]
```

---

# 11. filter()

Returns matching elements.

```js
const nums = [1,2,3,4];

const even =
nums.filter(
    num => num % 2 === 0
);
```

Output:

```js
[2,4]
```

---

# 12. reduce()

Reduces array to single value.

```js
const nums = [1,2,3,4];

const sum =
nums.reduce(
    (acc,curr)=>acc+curr,
    0
);
```

Output:

```text
10
```

---

# 13. find()

Returns first matching element.

```js
const users = [
    {id:1},
    {id:2}
];

const user =
users.find(
    user => user.id === 2
);
```

---

# 14. findIndex()

Returns matching index.

```js
users.findIndex(
    user => user.id === 2
);
```

---

# 15. some()

Checks if at least one element matches.

```js
const nums = [1,2,3];

nums.some(
    num => num > 2
);
```

Output:

```text
true
```

---

# 16. every()

Checks if all elements match.

```js
nums.every(
    num => num > 0
);
```

Output:

```text
true
```

---

# 17. sort()

```js
const nums = [4,2,8,1];

nums.sort();
```

Wrong output:

```js
[1,2,4,8]
```

Works here accidentally.

Correct numeric sorting:

```js
nums.sort(
    (a,b)=>a-b
);
```

Ascending.

```js
nums.sort(
    (a,b)=>b-a
);
```

Descending.

---

# 18. reverse()

```js
arr.reverse();
```

---

# 19. slice()

Returns portion of array.

```js
const arr = [1,2,3,4];

arr.slice(1,3);
```

Output:

```js
[2,3]
```

Original array unchanged.

---

# 20. splice()

Modifies original array.

```js
arr.splice(1,2);
```

Removes elements.

---

Insert:

```js
arr.splice(1,0,100);
```

---

# 21. concat()

```js
const result =
arr1.concat(arr2);
```

---

# 22. join()

```js
arr.join("-");
```

Output:

```text
1-2-3
```

---

# 23. split()

String to array.

```js
const arr =
"hello world".split(" ");
```

Output:

```js
["hello","world"]
```

---

# 24. flat()

```js
const arr =
[1,[2,[3]]];

arr.flat(2);
```

Output:

```js
[1,2,3]
```

---

# 25. Array Destructuring

```js
const colors =
["red","blue"];

const [first,second] =
colors;
```

---

# 26. Spread Operator with Arrays

```js
const copy =
[...arr];
```

---

# OBJECTS

---

# 1. What is an Object?

Stores key-value pairs.

```js
const user = {
    name:"Krishna",
    age:20
};
```

---

# 2. Access Properties

## Dot Notation

```js
user.name
```

---

## Bracket Notation

```js
user["name"]
```

Useful when key is dynamic.

---

# 3. Add Properties

```js
user.city = "Delhi";
```

---

# 4. Update Properties

```js
user.age = 21;
```

---

# 5. Delete Properties

```js
delete user.age;
```

---

# 6. Nested Objects

```js
const user = {
    name:"Krishna",

    address:{
        city:"Delhi"
    }
};
```

Access:

```js
user.address.city
```

---

# 7. Object Destructuring

```js
const user = {
    name:"Krishna",
    age:20
};

const {name,age} = user;
```

---

# 8. Rename During Destructuring

```js
const {
    name:userName
} = user;
```

---

# 9. Default Values

```js
const {
    city="Delhi"
} = user;
```

---

# 10. Object Methods

```js
const user = {

    name:"Krishna",

    greet(){
        console.log("Hello");
    }
};
```

---

# 11. this Keyword

```js
const user = {

    name:"Krishna",

    greet(){
        console.log(this.name);
    }
};
```

---

# 12. Object.keys()

Returns keys.

```js
Object.keys(user);
```

Output:

```js
["name","age"]
```

---

# 13. Object.values()

Returns values.

```js
Object.values(user);
```

Output:

```js
["Krishna",20]
```

---

# 14. Object.entries()

Returns key-value pairs.

```js
Object.entries(user);
```

Output:

```js
[
 ["name","Krishna"],
 ["age",20]
]
```

---

# 15. Looping Objects

```js
for(const key in user){
    console.log(key);
}
```

---

# 16. Spread Operator with Objects

```js
const updated = {
    ...user,
    city:"Delhi"
};
```

---

# 17. Object.assign()

Copy objects.

```js
const copy =
Object.assign({},user);
```

---

# 18. Shallow Copy vs Deep Copy

## Shallow Copy

```js
const copy = {
    ...user
};
```

Nested objects still share references.

---

## Deep Copy

```js
const copy =
structuredClone(user);
```

---

# 19. Optional Chaining

```js
user?.address?.city
```

Avoids errors if property doesn't exist.

---

# 20. Nullish Coalescing

```js
const city =
user.city ?? "Unknown";
```

---

# Most Important Interview Topics

### Arrays

* push/pop
* shift/unshift
* map
* filter
* reduce
* find
* findIndex
* some
* every
* sort
* slice vs splice
* forEach
* array destructuring
* spread operator

### Objects

* Object creation
* Dot vs bracket notation
* Object destructuring
* this keyword
* Object.keys()
* Object.values()
* Object.entries()
* Spread operator
* Shallow vs Deep Copy
* Optional chaining

### Very Frequently Asked

1. map vs forEach
2. filter vs find
3. slice vs splice
4. Object.keys vs Object.values vs Object.entries
5. Shallow Copy vs Deep Copy
6. Dot vs Bracket Notation
7. this inside object methods
8. Array methods that mutate vs don't mutate
9. Array Destructuring
10. Object Destructuring

If this is for your internship curriculum, this covers essentially the full "Arrays & Objects" section expected before moving on to DOM, Events, Async JavaScript, React, or backend topics.
