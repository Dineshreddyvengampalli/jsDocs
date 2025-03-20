# Understanding Higher-Order Functions in JavaScript

In JavaScript, **higher-order functions (HOFs)** are functions that either:
- Take another function as an argument, or
- Return a function as their result.

Higher-order functions enable **functional programming**, **code reusability**, and **cleaner syntax**.

---
## 1. What are Higher-Order Functions?
A **higher-order function** is a function that operates on other functions, by:
1. **Accepting a function as an argument**
2. **Returning a function**

### **Example: Function as an Argument**
```js
function greet(name, formatter) {
    console.log(formatter(name));
}

function toUpperCase(name) {
    return name.toUpperCase();
}

greet("Alice", toUpperCase); // ALICE
```
Here, `greet` is a **higher-order function** because it **accepts another function (`formatter`) as an argument**.

---
## 2. Built-in Higher-Order Functions
JavaScript provides **many built-in higher-order functions**, including:
- `map()`
- `filter()`
- `reduce()`
- `forEach()`

### **Example: Using `map()`**
`map()` transforms each element in an array using a callback function.
```js
const numbers = [1, 2, 3, 4];
const squared = numbers.map(num => num * num);
console.log(squared); // [1, 4, 9, 16]
```

### **Example: Using `filter()`**
`filter()` returns a new array with elements that satisfy a condition.
```js
const ages = [10, 15, 22, 30];
const adults = ages.filter(age => age >= 18);
console.log(adults); // [22, 30]
```

### **Example: Using `reduce()`**
`reduce()` accumulates values in an array into a single result.
```js
const nums = [1, 2, 3, 4];
const sum = nums.reduce((acc, num) => acc + num, 0);
console.log(sum); // 10
```

---
## 3. Returning Functions from Functions
A **higher-order function** can also return a function.

### **Example: Function Returning Another Function**
```js
function multiplyBy(factor) {
    return function (num) {
        return num * factor;
    };
}

const double = multiplyBy(2);
console.log(double(5)); // 10
console.log(double(10)); // 20
```
Here, `multiplyBy(2)` returns a new function that **multiplies numbers by 2**.

---
## 4. Custom Higher-Order Functions
You can create your own higher-order functions to handle reusable logic.

### **Example: Custom Function Executor**
```js
function execute(fn, a, b) {
    return fn(a, b);
}

function add(x, y) {
    return x + y;
}

console.log(execute(add, 5, 3)); // 8
```
`execute` is a **higher-order function** that calls any function (`fn`) with two arguments.

---
## 5. Benefits of Higher-Order Functions
- **Code Reusability** – Write general-purpose functions.
- **Modularity** – Keep functions separate and clean.
- **Functional Programming** – Use callbacks to write declarative code.
- **Improved Readability** – Replace loops with `.map()`, `.filter()`, `.reduce()`.

---
## 6. Summary
- **Higher-order functions** take or return other functions.
- JavaScript has built-in HOFs like `map()`, `filter()`, and `reduce()`.
- **Returning functions** allows for powerful customization.
- **Higher-order functions** simplify functional programming and improve maintainability.

Mastering higher-order functions makes JavaScript code more **efficient, readable, and reusable**!
