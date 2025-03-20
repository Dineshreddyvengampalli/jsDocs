# Understanding First-Class Functions in JavaScript

JavaScript treats functions as **first-class citizens**, meaning functions can be:
- Assigned to variables
- Passed as arguments to other functions
- Returned from other functions
- Stored in data structures like arrays or objects

This flexibility makes JavaScript **highly dynamic and functional programming-friendly**.

---
## 1. What are First-Class Functions?
A **first-class function** is a function that is treated like any other value. This means:
1. **Functions can be assigned to variables**
2. **Functions can be passed as arguments**
3. **Functions can be returned from other functions**

### **Example: Assigning a Function to a Variable**
```js
const greet = function() {
    console.log("Hello, World!");
};
greet(); // Output: Hello, World!
```
Here, `greet` holds an **anonymous function**, and calling `greet()` executes it.

---
## 2. Passing Functions as Arguments (Higher-Order Functions)
Functions can be passed as arguments to other functions. These are called **higher-order functions**.

### **Example: Passing a Function as an Argument**
```js
function executeFunction(fn) {
    fn(); // Executes the passed function
}

function sayHello() {
    console.log("Hello from function!");
}

executeFunction(sayHello);
```
### **Output:**
```
Hello from function!
```
Here, `executeFunction` takes another function as an argument and calls it inside.

---
## 3. Returning Functions from Functions
A function can return another function, enabling **function factories** and closures.

### **Example: Function Returning Another Function**
```js
function multiplyBy(factor) {
    return function (number) {
        return number * factor;
    };
}

const double = multiplyBy(2);
console.log(double(5)); // 10
console.log(double(10)); // 20
```
Here, `multiplyBy(2)` returns a function that multiplies any number by 2.

---
## 4. Storing Functions in Data Structures
Functions can be stored in arrays or objects.

### **Example: Storing Functions in an Object**
```js
const mathOperations = {
    add: function(a, b) { return a + b; },
    subtract: function(a, b) { return a - b; }
};

console.log(mathOperations.add(5, 3)); // 8
console.log(mathOperations.subtract(5, 3)); // 2
```

### **Example: Storing Functions in an Array**
```js
const operations = [
    function(a, b) { return a + b; },
    function(a, b) { return a - b; }
];
console.log(operations[0](10, 5)); // 15 (Addition)
console.log(operations[1](10, 5)); // 5 (Subtraction)
```

---
## 5. First-Class Functions Enable Functional Programming
Since JavaScript functions behave as **first-class citizens**, we can use **functional programming** concepts like:
- **Higher-order functions** (`map`, `filter`, `reduce`)
- **Closures**
- **Currying**

### **Example: Using `map` (Higher-Order Function)**
```js
const numbers = [1, 2, 3, 4];
const doubled = numbers.map(num => num * 2);
console.log(doubled); // [2, 4, 6, 8]
```
Here, `map()` takes a function as an argument and applies it to each array element.

---
## 6. Summary
- **First-class functions** allow treating functions like any other variable.
- **Functions can be assigned, passed, and returned**.
- **Higher-order functions** accept or return functions.
- **First-class functions enable functional programming**.

By understanding first-class functions, you can write more **flexible, reusable, and modular** JavaScript code!

