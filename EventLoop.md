# Understanding JavaScript Event Loop

JavaScript is a single-threaded, non-blocking, asynchronous language that uses an event loop to handle multiple tasks efficiently. The event loop is a crucial concept that helps manage asynchronous operations like callbacks, promises, and setTimeout().

## 1. What is the Event Loop?
The **event loop** is a mechanism that continuously checks the call stack to determine if there are pending tasks in the **callback queue** or **microtask queue** that need to be executed. It ensures JavaScript remains non-blocking by handling operations asynchronously.

## 2. JavaScript Execution Model
JavaScript operates on a **single-threaded** execution model, meaning it can execute only one task at a time. However, it achieves concurrency using:

- **Call Stack**: Manages function execution.
- **Web APIs**: Handles asynchronous operations (e.g., `setTimeout`, `fetch`, event listeners).
- **Task Queues**: Stores asynchronous callbacks to be executed later.
- **Event Loop**: Continuously checks if the call stack is empty and pushes queued tasks to it.

## 3. How the Event Loop Works
1. JavaScript executes synchronous code first, using the **call stack**.
2. When an asynchronous operation (e.g., `setTimeout`, API call) is encountered, it is delegated to the **Web API**.
3. Once the operation completes, the callback is added to the **callback queue** (for `setTimeout`) or **microtask queue** (for Promises, `process.nextTick` in Node.js).
4. The **event loop** checks if the **call stack** is empty.
5. If the stack is empty, it pushes tasks from the **microtask queue** first, then from the **callback queue**.
6. The cycle repeats indefinitely.

## 4. Components of the Event Loop
### **Call Stack**
The **call stack** follows a Last In, First Out (LIFO) structure and executes functions in order.

Example:
```js
function first() {
    console.log("First function");
}
function second() {
    console.log("Second function");
    first();
}
second();
console.log("End of script");
```
Execution order:
```
1. Call `second()` → Added to stack
2. `console.log("Second function")` executes
3. Call `first()` → Added to stack
4. `console.log("First function")` executes
5. `first()` returns, removed from stack
6. `second()` returns, removed from stack
7. `console.log("End of script")` executes
```

### **Web APIs**
Web APIs handle asynchronous operations like:
- `setTimeout()`
- `setInterval()`
- `fetch()`
- DOM events

Example:
```js
console.log("Start");
setTimeout(() => console.log("Timeout Callback"), 2000);
console.log("End");
```
Output order:
```
1. "Start"
2. "End"
3. After 2 seconds: "Timeout Callback"
```

### **Callback Queue (Macrotask Queue)**
Stores callbacks from:
- `setTimeout`
- `setInterval`
- DOM events
- I/O operations

Callbacks are executed after the **microtask queue** is empty.

### **Microtask Queue**
Stores higher-priority tasks like:
- Promises (`.then`, `.catch`, `.finally`)
- `process.nextTick()` (Node.js)
- Mutation observers

Microtasks execute **before** macrotasks (callback queue tasks).

Example:
```js
console.log("Start");
setTimeout(() => console.log("Timeout Callback"), 0);
Promise.resolve().then(() => console.log("Promise Resolved"));
console.log("End");
```
Execution order:
```
1. "Start"
2. "End"
3. "Promise Resolved" (Microtask queue first)
4. "Timeout Callback" (Macrotask queue second)
```

## 5. Practical Example
```js
console.log("Start");
setTimeout(() => console.log("setTimeout"), 0);
Promise.resolve().then(() => console.log("Promise"));
console.log("End");
```
Execution order:
1. "Start"
2. "End"
3. "Promise" (Microtask queue executes first)
4. "setTimeout" (Macrotask queue executes after microtasks)

## 6. Event Loop in Node.js
Node.js uses a similar event loop but has different task queues:
- **Timers Queue**: Handles `setTimeout` and `setInterval`.
- **I/O Queue**: Handles file system and network I/O operations.
- **Check Queue**: Handles `setImmediate()`.
- **Close Queue**: Handles socket close events.
- **Microtask Queue**: Processes `process.nextTick()` before Promises.

Example:
```js
setImmediate(() => console.log("setImmediate"));
process.nextTick(() => console.log("nextTick"));
```
Output:
```
nextTick
setImmediate
```

## 7. Summary
- The **event loop** allows JavaScript to handle asynchronous operations efficiently.
- The **call stack** executes synchronous code.
- The **Web APIs** handle async operations.
- The **microtask queue** executes before the **callback queue**.
- Understanding the event loop helps avoid unexpected behavior in asynchronous JavaScript code.

By mastering these concepts, you can write more efficient and predictable JavaScript applications.

