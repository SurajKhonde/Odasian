1. **Primitive Data Types**
These are the basic building blocks. They are **immutable** and stored by **value**.



2. **Classic `for` loop**
```javascript
for (let i = 0; i < 5; i++) {
  console.log(i);
}

```
2. **`for...of` loop**
Used to iterate **over iterable objects** like arrays, strings, maps, sets, etc.
```javascript
const arr = ['a', 'b', 'c'];
for (const item of arr) {
  console.log(item);
}

```
3. **`for...in` loop**
Used to iterate **over enumerable properties** (keys) of an object.
```javascript
const obj = { a: 1, b: 2 };
for (const key in obj) {
  console.log(key, obj[key]);
}

```
4. **`Array.prototype.forEach()`**
Method to loop over arrays using a callback.
```javascript
const nums = [1, 2, 3];
nums.forEach((num, index) => {
  console.log(index, num);
});

```
5. **`while` loop**
```javascript
let i = 0;
while (i < 5) {
  console.log(i);
  i++;
}

```
6. **`do...while` loop**
 Executes the block **at least once**, then checks the condition.
```javascript
let i = 0;
do {
  console.log(i);
  i++;
} while (i < 5);

```
7. **`map()`**
Used for transforming arrays and returning a new one.
```javascript
const nums = [1, 2, 3];
const squared = nums.map(num => num * num);
console.log(squared);

```
**Primitive Data Types in JavaScript**

| **Type**    | **Example**     | **Description**                         |
| ----------- | --------------- | --------------------------------------- |
| `String`    | `'hello'`       | Sequence of characters (text values)    |
| `Number`    | `42`, `3.14`    | Integer and floating-point numbers      |
| `Boolean`   | `true`, `false` | Logical values (true or false)          |
| `undefined` | `let x;`        | Declared but not assigned a value       |
| `null`      | `let y = null;` | Intentional absence of any object value |
| `BigInt`    | `123n`          | For very large integers                 |
| `Symbol`    | `Symbol('id')`  | Unique and immutable identifiers        |
**Non-Primitive (Reference) Data Types**

| Type                   | Example                | Description          |
| ---------------------- | ---------------------- | -------------------- |
| `Object`               | `{name: "John"}`       | Key-value pairs      |
| `Array`                | `[1, 2, 3]`            | Ordered elements     |
| `Function`             | `function() {}`        | Reusable code blocks |
| `Date`, `RegExp`, etc. | Other built-in objects |                      |
**Key Points**:
- Stored in the **heap**, reference stored in the **stack**.
- Compared by **reference**.
- Mutable (can be changed even if declared with `const`).

### **Primitive vs Non-Primitive (Reference) in JavaScript**

|**Feature**|**Primitive**|**Non-Primitive (Reference)**|
|---|---|---|
|**Stored as**|Value|Reference|
|**Stored in**|Stack|Heap (reference is in the stack)|
|**Mutability**|Immutable|Mutable|
|**Comparison**|Compared by value|Compared by reference|
|**Examples**|`string`, `number`, `boolean`, `undefined`, `null`, `bigint`, `symbol`|`object`, `array`, `function`|
|**Memory efficiency**|More efficient|Less efficient (can grow large)|
>[!info]
>Even `null` is considered a primitive, but it returns `"object"` when checked with `typeof`. This is a **long-standing bug** in JavaScript.

`typeof null // "object"`

**String Methods in JavaScript**
##  JavaScript String Methods

| Method                        | Description                                 | Example                                        |
| ----------------------------- | ------------------------------------------- | ---------------------------------------------- |
| `.length`                     | Returns length of string                    | `'hello'.length // 5`                          |
| `.charAt(index)`              | Returns character at specific index         | `'hello'.charAt(1) // 'e'`                     |
| `.at(index)`                  | Similar to charAt (supports negative index) | `'hello'.at(-1) // 'o'`                        |
| `.slice(start, end)`          | Extracts part of string                     | `'hello'.slice(1, 4) // 'ell'`                 |
| `.substring(start, end)`      | Similar to slice (no negative index)        | `'hello'.substring(1, 4) // 'ell'`             |
| `.substr(start, length)`      | Extracts substring (**deprecated)**         | `'hello'.substr(1, 3) // 'ell'`                |
| `.toUpperCase()`              | Converts to uppercase                       | `'hello'.toUpperCase() // 'HELLO'`             |
| `.toLowerCase()`              | Converts to lowercase                       | `'HELLO'.toLowerCase() // 'hello'`             |
| `.trim()`                     | Removes whitespace from both ends           | `' hi '.trim() // 'hi'`                        |
| `.trimStart()` / `.trimEnd()` | Trims start or end only                     | `' hi '.trimStart() // 'hi '`                  |
| `.includes(sub)`              | Checks if string contains substring         | `'hello'.includes('ell') // true`              |
| `.startsWith(sub)`            | Checks if string starts with given text     | `'hello'.startsWith('he') // true`             |
| `.endsWith(sub)`              | Checks if string ends with given text       | `'hello'.endsWith('lo') // true`               |
| `.indexOf(sub)`               | Returns first index of match or -1          | `'hello'.indexOf('l') // 2`                    |
| `.lastIndexOf(sub)`           | Returns last index of match or -1           | `'hello'.lastIndexOf('l') // 3`                |
| `.replace(old, new)`          | Replaces first match                        | `'hello'.replace('l', 'L') // 'heLlo'`         |
| `.replaceAll(old, new)`       | Replaces all matches                        | `'lollipop'.replaceAll('l', 'L') // 'LoLipop'` |
| `.repeat(n)`                  | Repeats the string n times                  | `'ha'.repeat(3) // 'hahaha'`                   |
| `.split(separator)`           | Splits string into array                    | `'a,b,c'.split(',') // ['a','b','c']`          |
| `.concat(str)`                | Joins two strings                           | `'Hello'.concat(' World') // 'Hello World'`    |
| `.match(regex)`               | Matches string against regex                | `'abc123'.match(/\\d+/) // ['123']`            |
| `.padStart(length, pad)`      | Pads at the beginning                       | `'5'.padStart(3, '0') // '005'`                |
| `.padEnd(length, pad)`        | Pads at the end                             | `'5'.padEnd(3, '0') // '500'`                  |
### `.length` is a **property**, **not** a method.
- **Properties** return a value directly.
- **Methods** are functions attached to an object — you call them with `()`.
### Number Methods & Properties
## 🔢 JavaScript Number Methods & Properties

| Method / Property         | Description                                     | Example                              |
|---------------------------|-------------------------------------------------|--------------------------------------|
| `Number()`                | Converts a value to a number                    | `Number('42') // 42`                 |
| `parseInt(string)`        | Parses and returns an integer                   | `parseInt('10.5') // 10`             |
| `parseFloat(string)`      | Parses and returns a floating-point number      | `parseFloat('10.5') // 10.5`         |
| `.toFixed(n)`             | Returns string with fixed `n` decimal places    | `(3.14159).toFixed(2) // '3.14'`     |
| `.toPrecision(n)`         | Formats number to `n` significant digits        | `(3.14159).toPrecision(3) // '3.14'` |
| `.toString(base)`         | Converts number to a string (optionally in base)| `(255).toString(16) // 'ff'`         |
| `.valueOf()`              | Returns the primitive value of a Number object  | `(42).valueOf() // 42`               |
| `isNaN(value)`            | Checks if value is NaN                          | `isNaN('abc') // true`               |
| `Number.isNaN(value)`     | Strict check for NaN (doesn't coerce types)     | `Number.isNaN(NaN) // true`          |
| `Number.isInteger(value)` | Checks if value is an integer                   | `Number.isInteger(4) // true`        |
| `Number.isFinite(value)`  | Checks if value is finite                       | `Number.isFinite(100) // true`       |
| `Math.round()`            | Rounds to nearest integer                       | `Math.round(4.6) // 5`               |
| `Math.floor()`            | Rounds down                                     | `Math.floor(4.9) // 4`               |
| `Math.ceil()`             | Rounds up                                       | `Math.ceil(4.1) // 5`                |
| `Math.trunc()`            | Removes decimal part                            | `Math.trunc(4.9) // 4`               |

###### *Few Number **Constants** in JavaScript*
| Property              | Description                            | Example                      |
|-----------------------|----------------------------------------|------------------------------|
| `Number.MAX_VALUE`    | Largest possible number                | `1.7976931348623157e+308`    |
| `Number.MIN_VALUE`    | Smallest positive number               | `5e-324`                     |
| `Number.POSITIVE_INFINITY` | Represents +Infinity             | `Number.POSITIVE_INFINITY`  |
| `Number.NEGATIVE_INFINITY` | Represents -Infinity             | `Number.NEGATIVE_INFINITY`  |
| `Number.NaN`          | Not a Number                           | `Number.NaN`                 |
##### JavaScript Array Methods
##  JavaScript Array Methods

| Method                                  | Description                                | Example                                     |
| --------------------------------------- | ------------------------------------------ | ------------------------------------------- |
| `.length`                               | Returns number of elements                 | `[1, 2, 3].length // 3`                     |
| `.push(item)`                           | Adds item to end                           | `[1, 2].push(3) // [1, 2, 3]`               |
| `.pop()`                                | Removes last item                          | `[1, 2, 3].pop() // [1, 2]`                 |
| `.unshift(item)`                        | Adds item to beginning                     | `[2, 3].unshift(1) // [1, 2, 3]`            |
| `.shift()`                              | Removes first item                         | `[1, 2, 3].shift() // [2, 3]`               |
| `.concat(arr)`                          | Merges arrays                              | `[1].concat([2, 3]) // [1, 2, 3]`           |
| `.join(separator)`                      | Converts array to string                   | `[1, 2].join('-') // '1-2'`                 |
| `.slice(start, end)`                    | Extracts part of array                     | `[1, 2, 3].slice(1, 3) // [2, 3]`           |
| `.splice(start, deleteCount, ...items)` | Removes/replaces/adds items                | `[1, 2, 3].splice(1, 1, 4) // [1, 4, 3]`    |
| `.indexOf(item)`                        | First index of item                        | `[1, 2, 3].indexOf(2) // 1`                 |
| `.lastIndexOf(item)`                    | Last index of item                         | `[1, 2, 2, 3].lastIndexOf(2) // 2`          |
| `.includes(item)`                       | Checks if item exists                      | `[1, 2].includes(2) // true`                |
| `.reverse()`                            | Reverses the array in place                | `[1, 2].reverse() // [2, 1]`                |
| `.sort()`                               | Sorts array (as strings by default)        | `[3, 1, 2].sort() // [1, 2, 3]`             |
| `.fill(value, start, end)`              | Fills part of array                        | `[1, 2, 3].fill(0, 1, 2) // [1, 0, 3]`      |
| `.flat(depth)`                          | Flattens nested arrays                     | `[1, [2, [3]]].flat(2) // [1, 2, 3]`        |
| `.toString()`                           | Converts array to comma-separated string   | `[1, 2].toString() // '1,2'`                |
| `.find(callback)`                       | Returns first match                        | `[1, 2, 3].find(x => x > 1) // 2`           |
| `.findIndex(callback)`                  | Returns index of first match               | `[1, 2, 3].findIndex(x => x > 1) // 1`      |
| `.filter(callback)`                     | Returns array of matches                   | `[1, 2, 3].filter(x => x > 1) // [2, 3]`    |
| `.map(callback)`                        | Transforms array                           | `[1, 2].map(x => x * 2) // [2, 4]`          |
| `.forEach(callback)`                    | Iterates over array                        | `[1, 2].forEach(x => console.log(x))`       |
| `.reduce(callback, initial)`            | Reduces to single value                    | `[1, 2, 3].reduce((a, b) => a + b, 0) // 6` |
| `.every(callback)`                      | Checks if all match condition              | `[1, 2, 3].every(x => x > 0) // true`       |
| `.some(callback)`                       | Checks if any match condition              | `[1, 2, 3].some(x => x > 2) // true`        |
| `.at(index)`                            | Returns item at index (supports negatives) | `[1, 2, 3].at(-1) // 3`                     |
| `Array.isArray(arr)`                    | Checks if value is array                   | `Array.isArray([1, 2]) // true`             |
A **callback** is simply a **function** that you pass into another function as an argument, which is then called (or executed) at a later time.
A **callback** is like saying, **"Hey, I’m giving you this function, call me back when you’re done!"**
```javascript
function greet(name) {
  console.log(`Hello, ${name}!`);
}
function processUserInput(callback) {
  const name = "Alice";
  callback(name); // Calls the passed-in function (greet) with 'name' as the argument
}
// Passing greet as a callback to processUserInput
processUserInput(greet);  // Output: Hello, Alice!
```
Object Methods
```javascript

```
### JavaScript Object Methods

| Method                                         | Description                                                                             | Example                                                |
| ---------------------------------------------- | --------------------------------------------------------------------------------------- | ------------------------------------------------------ |
| `Object.keys(obj)`                             | Returns an array of an object's own enumerable property names                           | `Object.keys({a: 1, b: 2}) // ['a', 'b']`              |
| `Object.values(obj)`                           | Returns an array of an object's own enumerable property values                          | `Object.values({a: 1, b: 2}) // [1, 2]`                |
| `Object.entries(obj)`                          | Returns an array of an object's own enumerable string-keyed property [key, value] pairs | `Object.entries({a: 1, b: 2}) // [['a', 1], ['b', 2]]` |
| `Object.assign(target, ...sources)`            | Copies all enumerable properties from one or more source objects to a target object     | `Object.assign({}, {a: 1}, {b: 2}) // {a: 1, b: 2}`    |
| `Object.freeze(obj)`                           | Freezes an object (makes it immutable)                                                  | `Object.freeze({a: 1})`                                |
| `Object.is(obj1, obj2)`                        | Compares if two values are the same (same value and type)                               | `Object.is(42, 42) // true`                            |
| `Object.create(proto)`                         | Creates a new object with the specified prototype object and properties                 | `Object.create({x: 1}) // {x: 1}`                      |
| `Object.hasOwn(obj, prop)`                     | Checks if an object has a property as its own property                                  | `Object.hasOwn({a: 1}, 'a') // true`                   |
| `Object.prototype.toString()`                  | Returns a string representation of the object                                           | `({}).toString() // '[object Object]'`                 |
| `Object.prototype.isPrototypeOf(obj)`          | Checks if an object is in the prototype chain of another                                | `Object.prototype.isPrototypeOf({a: 1}) // true`       |
| `Object.getPrototypeOf(obj)`                   | Returns the prototype of an object                                                      | `Object.getPrototypeOf({}) // Object.prototype`        |
| `Object.setPrototypeOf(obj, proto)`            | Sets the prototype (parent) of an object                                                | `Object.setPrototypeOf({}, Array.prototype)`           |
| `Object.defineProperty(obj, prop, descriptor)` | Defines a new property on an object with specific options                               | `Object.defineProperty({}, 'a', {value: 1})`           |
| `Object.defineProperties(obj, props)`          | Defines multiple properties on an object                                                | `Object.defineProperties({}, {a: {value: 1}})`         |
****

