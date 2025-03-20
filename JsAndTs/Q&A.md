# JavaScript Interview Questions and Answers

This document contains **tricky and frequently asked JavaScript interview questions** with detailed explanations and examples.

---
## 1. What is the difference between `==` and `===`?
### **Answer:**
- `==` (Loose Equality) compares values **without** considering type.
- `===` (Strict Equality) compares values **and** type.

```js
console.log(5 == "5");  // true (type coercion)
console.log(5 === "5"); // false (different types)
```
---
## 2. What is a Closure?
### **Answer:**
A **closure** is a function that remembers variables from its outer scope even after the outer function has finished execution.

```js
function outer() {
    let count = 0;
    return function inner() {
        count++;
        console.log(count);
    };
}

const increment = outer();
increment(); // 1
increment(); // 2
```
Here, `inner()` retains access to `count` even after `outer()` has executed.

---
## 3. What is the Event Loop in JavaScript?
### **Answer:**
The **Event Loop** allows JavaScript to handle asynchronous tasks **non-blockingly**.

```js
console.log("Start");
setTimeout(() => console.log("Timeout"), 0);
Promise.resolve().then(() => console.log("Promise"));
console.log("End");
```
### **Output:**
```
Start
End
Promise
Timeout
```
- **Synchronous code** runs first (`Start`, `End`).
- **Microtasks (`Promise.then`) execute before macrotasks (`setTimeout`).**

---
## 4. What is Hoisting?
### **Answer:**
**Hoisting** moves function and variable declarations to the top of their scope before execution.

```js
console.log(x); // undefined
var x = 10;
```
With `let` and `const`, accessing before declaration gives an **error**:
```js
console.log(y); // ReferenceError
let y = 20;
```

---
## 5. What is the difference between `var`, `let`, and `const`?
### **Answer:**
| Feature | `var` | `let` | `const` |
|---------|------|------|--------|
| Scope | Function | Block | Block |
| Hoisting | Yes (initialized as `undefined`) | Yes (uninitialized) | Yes (uninitialized) |
| Reassignable | Yes | Yes | No |
| Redeclarable | Yes | No | No |

---
## 6. What are `map()`, `filter()`, and `reduce()`?
### **Answer:**
- **`map()`** transforms each element and returns a new array.
- **`filter()`** returns elements that meet a condition.
- **`reduce()`** accumulates elements into a single value.

```js
const nums = [1, 2, 3, 4];
console.log(nums.map(n => n * 2)); // [2, 4, 6, 8]
console.log(nums.filter(n => n % 2 === 0)); // [2, 4]
console.log(nums.reduce((sum, n) => sum + n, 0)); // 10
```

---
## 7. What is Debouncing and Throttling?
### **Answer:**
**Debouncing** ensures a function executes only **after a delay**.
```js
function debounce(func, delay) {
    let timer;
    return function() {
        clearTimeout(timer);
        timer = setTimeout(() => func.apply(this, arguments), delay);
    };
}
```
**Throttling** ensures a function executes **at most once per interval**.
```js
function throttle(func, limit) {
    let inThrottle;
    return function() {
        if (!inThrottle) {
            func.apply(this, arguments);
            inThrottle = true;
            setTimeout(() => inThrottle = false, limit);
        }
    };
}
```

---
## 8. Additional Tricky JavaScript Questions
### **8.1. What will be the output of the following?**
```js
console.log(typeof NaN);
console.log(NaN === NaN);
```
**Output:**
```
"number"
false
```
**Explanation:** `NaN` is a special value of type `number`, but it is **not equal to itself**.

### **8.2. What happens when you use `setTimeout` with `0` milliseconds?**
```js
console.log("Start");
setTimeout(() => console.log("Inside Timeout"), 0);
console.log("End");
```
**Output:**
```
Start
End
Inside Timeout
```
Even though the delay is `0`, `setTimeout` moves to the callback queue and executes after the main thread is clear.

### **8.3. How do you check if an object is empty?**
```js
const obj = {};
console.log(Object.keys(obj).length === 0); // true
```
**Explanation:** `Object.keys(obj)` returns an array of keys. If the length is `0`, the object is empty.

### **8.4. What happens when you add properties to `__proto__`?**
```js
let obj = {};
obj.__proto__.test = "Added to prototype";
console.log({}.test);
```
**Output:**
```
"Added to prototype"
```
**Explanation:** The property is added to the `Object.prototype` and is accessible in all objects.

---
## 9. Summary
- Understand **Closures, Hoisting, Event Loop, and Scope**.
- Know the differences between `==` vs `===`, `null` vs `undefined`, and `var` vs `let` vs `const`.
- Be familiar with **map(), filter(), reduce(), debouncing, and throttling**.
- Know how to use **`call()`, `apply()`, and `bind()`**.
- Learn how `this` works and how to **deep clone objects**.
- Practice tricky JavaScript behaviors like `NaN`, `setTimeout(0)`, and `__proto__` properties.

