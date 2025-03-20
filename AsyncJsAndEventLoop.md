# Understanding Asynchronous JavaScript and Event Loop

JavaScript is a **single-threaded, non-blocking, asynchronous** programming language. It uses an **event loop** to handle multiple tasks efficiently without blocking execution.

---
## 1. What is Asynchronous JavaScript?
Asynchronous JavaScript allows operations like **API requests, file reading, and timers** to execute **without blocking** the main thread.

### **Example: Synchronous vs Asynchronous Execution**
#### **Synchronous Code (Blocking)**
```js
console.log("Start");
for (let i = 0; i < 1000000000; i++) {} // Long task
console.log("End");
```
**Output:**
```
Start
(wait for loop to finish)
End
```
The **loop blocks** further execution until completed.

#### **Asynchronous Code (Non-Blocking)**
```js
console.log("Start");
setTimeout(() => console.log("Inside Timeout"), 2000);
console.log("End");
```
**Output:**
```
Start
End
(after 2 seconds)
Inside Timeout
```
Here, `setTimeout` **delays execution** but does not block the main thread.

---
## 2. Event Loop in JavaScript
The **Event Loop** manages asynchronous operations by checking the **Call Stack** and moving tasks from the **Callback Queue** or **Microtask Queue** when the stack is empty.

### **How the Event Loop Works**
1. JavaScript runs **synchronous code first** (Call Stack execution).
2. Asynchronous tasks (e.g., `setTimeout`, `fetch`) go to **Web APIs**.
3. Once completed, their callbacks move to **Callback Queue** (macrotasks) or **Microtask Queue** (higher priority).
4. The **event loop** checks if the **Call Stack is empty** before executing queued tasks.

### **Example: Event Loop in Action**
```js
console.log("Start");

setTimeout(() => console.log("Timeout Callback"), 0);

Promise.resolve().then(() => console.log("Promise Resolved"));

console.log("End");
```
### **Execution Order:**
```
Start
End
Promise Resolved
Timeout Callback
```
- **Synchronous** code executes first (`Start`, `End`).
- **Microtasks (`Promise.then`) run before macrotasks (`setTimeout`)**.
- **Event loop moves `setTimeout` callback only after the call stack is empty.**

---
## 3. Callback Queue vs Microtask Queue
### **1. Callback Queue (Macrotasks)**
Includes:
- `setTimeout`
- `setInterval`
- DOM Events

### **2. Microtask Queue (Higher Priority)**
Includes:
- Promises (`.then()`, `.catch()`)
- `MutationObserver`
- `process.nextTick()` (Node.js)

### **Example:**
```js
setTimeout(() => console.log("Macrotask - setTimeout"), 0);
Promise.resolve().then(() => console.log("Microtask - Promise"));
console.log("Synchronous Log");
```
### **Execution Order:**
```
Synchronous Log
Microtask - Promise
Macrotask - setTimeout
```
**Microtasks execute before macrotasks!**

---
## 4. Asynchronous JavaScript with Promises & Async/Await
### **Using Promises**
```js
fetch("https://jsonplaceholder.typicode.com/todos/1")
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.log(error));
```
Promises avoid **callback hell** by chaining `.then()` calls.

### **Using Async/Await (More Readable)**
```js
async function fetchData() {
    try {
        let response = await fetch("https://jsonplaceholder.typicode.com/todos/1");
        let data = await response.json();
        console.log(data);
    } catch (error) {
        console.log(error);
    }
}
fetchData();
```
**`await` pauses execution until the promise resolves.**

---
## 5. Summary
- **Asynchronous JavaScript** allows non-blocking execution.
- The **Event Loop** manages tasks via the **Call Stack, Web APIs, and Task Queues**.
- **Microtasks (`Promise.then()`) execute before macrotasks (`setTimeout()`).**
- **Async/Await** simplifies handling asynchronous operations.

Understanding async JavaScript and the event loop helps **write efficient, non-blocking code**!

