# Understanding JavaScript Execution Context

JavaScript is a single-threaded, synchronous language that executes code within an execution context. Understanding execution contexts is crucial for mastering JavaScript's behavior, especially in relation to variable scope, hoisting, and the call stack.

## 1. What is an Execution Context?
An **Execution Context** is an abstract concept that represents the environment in which JavaScript code is evaluated and executed. Each execution context has three main components:

- **Variable Object (VO):** Stores function arguments, variable declarations, and function declarations.
- **Scope Chain:** Determines the accessibility of variables and functions.
- **`this` Binding:** Refers to the object that the function is executed in.

### Types of Execution Contexts
1. **Global Execution Context (GEC):** Created when a JavaScript file is executed. There is only one global execution context.
2. **Function Execution Context (FEC):** Created whenever a function is invoked.
3. **Eval Execution Context:** Created when `eval()` is executed (not commonly used).

## 2. Phases of Execution Context
An execution context is created in two phases:

### **1. Creation Phase**
- **Global Execution Context (GEC) is created.**
- A global object (`window` in browsers, `global` in Node.js) is created.
- `this` is assigned to the global object.
- Memory is allocated for variables and functions (hoisting occurs).
- Functions are stored in memory entirely, while variables are initialized as `undefined`.

Example:
```js
console.log(a); // undefined
var a = 10;
console.log(a); // 10

function greet() {
    console.log("Hello, World!");
}

greet(); // Hello, World!
```

### **2. Execution Phase**
- Code is executed line by line.
- Variables are assigned values.
- Functions are executed when called.

## 3. Call Stack and Function Execution
JavaScript maintains an execution stack (call stack) to manage function calls.

### **How the Call Stack Works**
1. When a script starts, the Global Execution Context (GEC) is pushed to the stack.
2. When a function is called, a new execution context is created and pushed to the stack.
3. When a function returns, its execution context is removed (popped) from the stack.
4. This continues until the stack is empty.

Example:
```js
function first() {
    console.log("First function");
    second();
    console.log("First function ends");
}

function second() {
    console.log("Second function");
}

first();
console.log("End of script");
```

### **Call Stack Execution:**
```
1. GEC is created
2. `first()` is called → New execution context pushed
3. `console.log("First function")` executes
4. `second()` is called → New execution context pushed
5. `console.log("Second function")` executes
6. `second()` execution context is popped
7. `console.log("First function ends")` executes
8. `first()` execution context is popped
9. `console.log("End of script")` executes
10. GEC is popped (script ends)
```

## 4. Hoisting
Hoisting is JavaScript’s behavior of moving function and variable declarations to the top of their scope before execution.

Example:
```js
console.log(x); // undefined
var x = 5;
console.log(x); // 5
```

Function hoisting:
```js
sayHello(); // "Hello!"

function sayHello() {
    console.log("Hello!");
}
```

Variables declared with `let` and `const` are hoisted but not initialized.
```js
console.log(y); // ReferenceError: Cannot access 'y' before initialization
let y = 10;
```

## 5. `this` Keyword in Execution Context
The value of `this` depends on how and where the function is invoked.

Example in global scope:
```js
console.log(this); // Window object (in browsers)
```

Example inside a function:
```js
function showThis() {
    console.log(this);
}
showThis(); // Window (in non-strict mode), undefined (in strict mode)
```

Example inside an object:
```js
const obj = {
    name: "John",
    greet: function() {
        console.log(this.name);
    }
};
obj.greet(); // John
```

## 6. Lexical Environment and Scope Chain
A **lexical environment** is a structure that holds variables and function declarations. It helps JavaScript resolve variable references through the **scope chain**.

Example:
```js
function outer() {
    let outerVar = "I am outer";

    function inner() {
        console.log(outerVar); // Accessible due to lexical scoping
    }
    inner();
}
outer();
```

## Summary
- **Execution context** consists of variable object, scope chain, and `this` binding.
- **Call stack** manages function execution.
- **Hoisting** moves declarations to the top of their scope.
- **Lexical scoping** ensures that functions access variables from their defining environment.

Understanding these concepts is crucial for writing efficient and bug-free JavaScript code.

