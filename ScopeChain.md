# Understanding JavaScript Scope Chain

JavaScript uses **scope chains** to determine variable accessibility in different contexts. Understanding scope chains is essential for writing efficient, bug-free JavaScript code.

## 1. What is Scope in JavaScript?
Scope defines **where variables can be accessed** in a program. JavaScript has three main types of scope:

1. **Global Scope** – Variables accessible from anywhere in the code.
2. **Function Scope** – Variables accessible only within a function.
3. **Block Scope** – Variables declared inside a block (`{}`) with `let` or `const`.

### **Example of Different Scopes:**
```js
var globalVar = "I am global";

function myFunction() {
    var functionVar = "I am inside a function";
    console.log(globalVar); // Accessible
    console.log(functionVar); // Accessible
}

myFunction();
console.log(globalVar); // Accessible
console.log(functionVar); // Error (function scope)
```
### **Output:**
```
I am global
I am inside a function
I am global
ReferenceError: functionVar is not defined
```

## 2. What is Scope Chain?
The **scope chain** is the mechanism by which JavaScript looks up variables **from inner to outer scopes**.

### **Example:**
```js
var a = "Global";

function outer() {
    var b = "Outer";
    function inner() {
        var c = "Inner";
        console.log(a); // Accessible (global scope)
        console.log(b); // Accessible (outer function scope)
        console.log(c); // Accessible (local scope)
    }
    inner();
}
outer();
```
### **Output:**
```
Global
Outer
Inner
```
JavaScript searches for variables **inside the function first**, then **moves outward** to the global scope.

## 3. How Scope Chain Works
- If a variable is **not found in the local function scope**, JavaScript searches **parent scopes**.
- If the variable is **not found anywhere**, JavaScript throws a **ReferenceError**.

### **Example:**
```js
function outer() {
    var x = "Outer variable";
    function inner() {
        console.log(x); // Found in the outer function scope
    }
    inner();
}
outer();
```
If `x` is not found inside `inner()`, JavaScript **looks up to `outer()`'s scope**.

## 4. Block Scope and Lexical Scope
### **Block Scope (`let` and `const`)**
Unlike `var`, `let` and `const` have **block scope**.

```js
if (true) {
    let blockVar = "I am block scoped";
    console.log(blockVar); // Accessible
}
console.log(blockVar); // ReferenceError (not accessible outside block)
```

### **Lexical Scope (Determined at Compile Time)**
Lexical scope means **functions can access variables where they were defined, not where they are called**.

```js
function outer() {
    let name = "Lexical";
    return function inner() {
        console.log(name);
    };
}

const closureFunction = outer();
closureFunction(); // Output: Lexical
```
Even though `inner()` is called outside `outer()`, it **retains access** to `name`.

## 5. Shadowing in Scope Chain
Variable **shadowing** occurs when a variable in an inner scope **overrides** a variable in an outer scope.

### **Example:**
```js
var a = "Global";
function myFunc() {
    var a = "Local";
    console.log(a); // Local (shadowed global `a`)
}
myFunc();
console.log(a); // Global
```
### **Output:**
```
Local
Global
```
The inner `a` **shadows** the global `a`, so `console.log(a)` inside `myFunc()` prints "Local".

## 6. Hoisting and Scope Chain
**Hoisting** moves variable and function declarations to the top of their scope **before execution**.

```js
console.log(x); // Undefined (due to hoisting)
var x = 5;
```
With `let` and `const`, variables remain in the **Temporal Dead Zone (TDZ)** until initialized.

```js
console.log(y); // ReferenceError (TDZ)
let y = 10;
```

## 7. Closures and Scope Chain
A **closure** is a function that retains access to its outer scope even after the outer function has executed.

```js
function counter() {
    let count = 0;
    return function increment() {
        count++;
        console.log(count);
    };
}

const add = counter();
add(); // 1
add(); // 2
```
The inner function **retains access** to `count`, forming a **closure**.

## 8. Summary
- **Scope chain** allows JavaScript to look up variables from inner to outer scopes.
- **Global scope** variables are accessible everywhere.
- **Function scope** variables are only accessible inside functions.
- **Block scope (`let`, `const`)** restricts variables to block `{}`.
- **Lexical scope** means functions remember their defining scope.
- **Shadowing** happens when an inner variable overrides an outer variable.
- **Closures** retain access to outer variables even after execution.

Understanding the **scope chain** is key to avoiding variable access issues and writing efficient JavaScript code!

