# Understanding Block Scope and Shadowing in JavaScript

JavaScript uses **block scope** to restrict variable access within `{}` blocks, and **shadowing** occurs when a variable in an inner scope has the same name as a variable in an outer scope.

---
## 1. Block Scope in JavaScript
**Block scope** means that variables declared inside a block `{}` **cannot be accessed from outside** the block.

### **Block Scope with `let` and `const`**
```js
if (true) {
    let a = 10;
    const b = 20;
    console.log(a, b); // 10 20 (accessible inside the block)
}
console.log(a, b); // ReferenceError: a is not defined
```
`a` and `b` are **only accessible inside the `if` block**.

### **No Block Scope with `var`**
Unlike `let` and `const`, `var` does **not** have block scope.
```js
if (true) {
    var c = 30;
}
console.log(c); // 30 (Accessible outside the block, which is unsafe)
```
**Best Practice:** Always use `let` and `const` for block-scoped variables.

---
## 2. Shadowing in JavaScript
**Shadowing** happens when a **local variable** with the same name as a variable in an **outer scope** **overrides** the outer variable within its scope.

### **Example of Variable Shadowing**
```js
let x = "Global";
function test() {
    let x = "Local";
    console.log(x); // "Local" (Inner x shadows outer x)
}
test();
console.log(x); // "Global" (Outer x remains unchanged)
```

The inner `x` **shadows** the global `x`, making the outer `x` **inaccessible** inside `test()`.

---
## 3. Shadowing with `var`, `let`, and `const`
### **Valid Shadowing (`let` → `let` or `const` → `const`)**
```js
let y = 50;
{
    let y = 100;
    console.log(y); // 100 (Inner `y` shadows outer `y`)
}
console.log(y); // 50 (Outer `y` is unaffected)
```

### **Illegal Shadowing (`var` cannot shadow `let` or `const`)**
```js
let z = 30;
{
    var z = 60; // SyntaxError: Identifier 'z' has already been declared
}
```
This is **not allowed** because `var` does not have block scope and tries to redeclare `z`.

---
## 4. Function Scope vs Block Scope
- **Function Scope:** Variables declared with `var` are **scoped to the function**.
- **Block Scope:** Variables declared with `let` and `const` are **scoped to the block `{}`**.

```js
function example() {
    if (true) {
        var m = "Function Scoped";
        let n = "Block Scoped";
    }
    console.log(m); // Works (function scoped)
    console.log(n); // ReferenceError (block scoped)
}
example();
```

---
## 5. Summary
- **Block Scope** restricts access to variables within `{}` (applies to `let` and `const`).
- **Shadowing** happens when an inner scope variable **overrides** an outer scope variable.
- `var` is function-scoped and **does not follow block scope**, leading to **potential bugs**.
- **Always use `let` and `const`** to avoid unintended scope issues.

By understanding block scope and shadowing, you can write safer and more predictable JavaScript code!
