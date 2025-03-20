# Understanding Callback Functions in JavaScript

A **callback function** is a function that is passed as an argument to another function and is executed later. Callbacks are widely used in **asynchronous programming**, event handling, and higher-order functions.

---
## 1. What is a Callback Function?
A **callback function** is a function passed to another function that gets called after some operation completes.

### **Example: Basic Callback Function**
```js
function greet(name, callback) {
    console.log("Hello, " + name);
    callback();
}

function sayGoodbye() {
    console.log("Goodbye!");
}

greet("Alice", sayGoodbye);
```
### **Output:**
```
Hello, Alice
Goodbye!
```
Here, `sayGoodbye` is passed as a callback and executes after `greet()` finishes.

---
## 2. Synchronous vs Asynchronous Callbacks
### **Synchronous Callback**
Executed immediately within the function.
```js
function calculate(a, b, callback) {
    return callback(a, b);
}

function add(x, y) {
    return x + y;
}

console.log(calculate(5, 3, add)); // 8
```

### **Asynchronous Callback**
Executed later, useful for API requests and timers.
```js
setTimeout(() => {
    console.log("This runs after 2 seconds");
}, 2000);
```

---
## 3. Callbacks in Higher-Order Functions
### **Using Callbacks with `forEach()`**
```js
const numbers = [1, 2, 3, 4];
numbers.forEach(num => console.log(num * 2));
```

### **Using Callbacks with `map()`**
```js
const squaredNumbers = numbers.map(num => num * num);
console.log(squaredNumbers); // [1, 4, 9, 16]
```

---
## 4. Callback Hell (Pyramid of Doom)
**Nested callbacks** lead to unreadable code.
```js
setTimeout(() => {
    console.log("Task 1 complete");
    setTimeout(() => {
        console.log("Task 2 complete");
        setTimeout(() => {
            console.log("Task 3 complete");
        }, 1000);
    }, 1000);
}, 1000);
```
This is **callback hell**, making debugging difficult.

---
## 5. Solution: Promises & Async/Await
Using **Promises** reduces callback hell.
```js
function wait(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}

async function runTasks() {
    await wait(1000);
    console.log("Task 1 complete");
    await wait(1000);
    console.log("Task 2 complete");
    await wait(1000);
    console.log("Task 3 complete");
}
runTasks();
```

---
## 6. Summary
- **Callbacks** allow functions to execute other functions.
- **Synchronous callbacks** run immediately; **asynchronous callbacks** run later.
- Callbacks are used in **higher-order functions** like `map()`, `forEach()`.
- **Callback Hell** happens with deeply nested callbacks.
- Use **Promises or Async/Await** to simplify callbacks.

Mastering callbacks is key to handling **asynchronous JavaScript** efficiently!

