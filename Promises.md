# Understanding JavaScript Promises

JavaScript **Promises** provide a cleaner way to handle asynchronous operations compared to traditional callback functions. They help in managing **asynchronous operations** like API requests, file reading, and timers efficiently, avoiding **callback hell**.

## 1. What is a Promise?
A **Promise** is an object that represents the eventual **completion** (or **failure**) of an asynchronous operation. It has three states:

1. **Pending** – Initial state, operation not completed.
2. **Fulfilled** – Operation completed successfully.
3. **Rejected** – Operation failed.

### **Basic Syntax of a Promise**
```js
const myPromise = new Promise((resolve, reject) => {
    let success = true; // Simulating success/failure
    if (success) {
        resolve("Operation Successful");
    } else {
        reject("Operation Failed");
    }
});
```

## 2. Consuming a Promise
We can consume a promise using `.then()`, `.catch()`, and `.finally()` methods.

```js
myPromise
    .then(result => console.log(result)) // Runs if resolved
    .catch(error => console.log(error))  // Runs if rejected
    .finally(() => console.log("Operation completed")); // Runs regardless
```

### **Output (if success is true):**
```
Operation Successful
Operation completed
```

## 3. Chaining Promises
Promises can be **chained** to handle multiple asynchronous operations sequentially.

```js
function asyncTask1() {
    return new Promise(resolve => {
        setTimeout(() => {
            console.log("Task 1 completed");
            resolve("Data from Task 1");
        }, 1000);
    });
}

function asyncTask2(previousData) {
    return new Promise(resolve => {
        setTimeout(() => {
            console.log("Task 2 completed");
            resolve(previousData + " -> Data from Task 2");
        }, 1000);
    });
}

asyncTask1()
    .then(data => asyncTask2(data))
    .then(finalData => console.log("Final Output:", finalData))
    .catch(error => console.log("Error:", error));
```

### **Output:**
```
Task 1 completed
Task 2 completed
Final Output: Data from Task 1 -> Data from Task 2
```

## 4. Handling Multiple Promises
### **Using `Promise.all()`**
Executes multiple promises in parallel and returns an array of results when all are resolved.
```js
const promise1 = new Promise(resolve => setTimeout(() => resolve("Result 1"), 2000));
const promise2 = new Promise(resolve => setTimeout(() => resolve("Result 2"), 1000));

Promise.all([promise1, promise2])
    .then(results => console.log("Results:", results))
    .catch(error => console.log("Error:", error));
```

### **Output:**
```
Results: ["Result 1", "Result 2"]
```

### **Using `Promise.race()`**
Returns the result of the first promise that resolves or rejects.
```js
Promise.race([promise1, promise2])
    .then(result => console.log("First resolved:", result))
    .catch(error => console.log("Error:", error));
```

### **Output:**
```
First resolved: Result 2
```

## 5. Async/Await (Better Way to Handle Promises)
`async/await` provides a more readable way to handle promises.

```js
async function fetchData() {
    try {
        const data1 = await asyncTask1();
        const data2 = await asyncTask2(data1);
        console.log("Final Data:", data2);
    } catch (error) {
        console.log("Error:", error);
    }
}
fetchData();
```

### **Output:**
```
Task 1 completed
Task 2 completed
Final Data: Data from Task 1 -> Data from Task 2
```

## 6. Error Handling with Async/Await
Handling errors with `try...catch` is cleaner compared to `.catch()`.

```js
async function fetchWithErrorHandling() {
    try {
        let response = await fetch("https://jsonplaceholder.typicode.com/posts/1");
        let data = await response.json();
        console.log(data);
    } catch (error) {
        console.error("Error fetching data:", error);
    }
}
fetchWithErrorHandling();
```

## 7. Summary
- **Promises** handle asynchronous operations in JavaScript.
- **States:** Pending → Fulfilled / Rejected.
- Use `.then()`, `.catch()`, `.finally()` to handle promises.
- Use `Promise.all()` for parallel execution and `Promise.race()` to get the first resolved promise.
- **Async/Await** simplifies working with promises.
- Always handle errors with `.catch()` or `try...catch`.

By mastering promises, you can write more **efficient**, **readable**, and **error-free** asynchronous JavaScript code!

