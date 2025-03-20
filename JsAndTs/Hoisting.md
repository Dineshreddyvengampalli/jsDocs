# Understanding JavaScript Hoisting

JavaScript **hoisting** is a behavior where variable and function declarations are moved to the top of their scope before execution. This means you can use variables and functions before declaring them in the code.

## 1. What is Hoisting?
Hoisting is JavaScript’s default behavior of moving declarations to the top of the scope during the execution phase. However, **only the declarations** are hoisted, not the initializations.

### Example:
```js
console.log(a); // Undefined
var a = 10;
console.log(a); // 10
```
Here, `var a;` is hoisted to the top, but `a = 10;` remains in place. The execution behaves as:
```js
var a;
console.log(a); // Undefined
a = 10;
console.log(a); // 10
```

## 2. Hoisting with `var`, `let`, and `const`
### **Using `var` (Hoisted but Undefined)**
Variables declared with `var` are hoisted and initialized with `undefined`.

Example:
```js
console.log(x); // Undefined
var x = 5;
console.log(x); // 5
```

### **Using `let` and `const` (Hoisted but Not Initialized)**
Variables declared with `let` and `const` are hoisted but **not initialized**. Accessing them before declaration results in a **ReferenceError** due to the **Temporal Dead Zone (TDZ)**.

Example:
```js
console.log(y); // ReferenceError: Cannot access 'y' before initialization
let y = 10;
```

### **Temporal Dead Zone (TDZ)**
The **TDZ** is the period between the start of the execution and the point where the variable is declared.

Example:
```js
console.log(z); // ReferenceError
const z = 20;
```
Here, `z` is hoisted but not initialized until the declaration line is reached.

## 3. Function Hoisting
Functions are **fully hoisted**, meaning they can be called before their declaration.

Example:
```js
sayHello(); // "Hello!"
function sayHello() {
    console.log("Hello!");
}
```
This works because function declarations are hoisted **along with their definitions**.

However, function expressions using `var`, `let`, or `const` are **not** hoisted the same way.

### **Function Expressions Are Not Hoisted**
```js
hello(); // TypeError: hello is not a function
var hello = function() {
    console.log("Hello!");
};
```
Here, `hello` is hoisted as `undefined`, but the function definition is not.

With `let` or `const`, an error occurs:
```js
greet(); // ReferenceError: Cannot access 'greet' before initialization
const greet = function() {
    console.log("Hi!");
};
```

## 4. Class Hoisting
Classes in JavaScript are **not hoisted** the same way as functions.

Example:
```js
const obj = new Person(); // ReferenceError: Cannot access 'Person' before initialization
class Person {
    constructor() {
        console.log("Person created");
    }
}
```
This happens because class declarations are hoisted but **not initialized**, similar to `let` and `const`.

## 5. Best Practices to Avoid Hoisting Issues
- Always declare variables at the beginning of their scope.
- Use `let` and `const` instead of `var` to avoid accidental hoisting issues.
- Declare functions before calling them.
- Avoid relying on hoisting behavior for cleaner, more predictable code.

## 6. Summary
- **Hoisting** moves declarations to the top but does not initialize them.
- `var` is hoisted with `undefined`, while `let` and `const` remain in the **Temporal Dead Zone**.
- **Function declarations** are hoisted entirely, but **function expressions** are not.
- **Classes are not hoisted** in a usable way.
- Understanding hoisting helps prevent unexpected behavior and debugging issues in JavaScript.

By keeping these points in mind, you can write more reliable and predictable JavaScript code!

