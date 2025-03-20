# Understanding `let` and `const` in JavaScript

In modern JavaScript (ES6+), `let` and `const` provide better ways to declare variables compared to `var`. They offer **block scope**, prevent **hoisting issues**, and help write more reliable code.

## 1. `let` vs `const` vs `var`
| Feature       | `var` | `let` | `const` |
|--------------|------|------|--------|
| Scope        | Function Scope | Block Scope | Block Scope |
| Hoisted      | Yes (initialized as `undefined`) | Yes (not initialized) | Yes (not initialized) |
| Reassignable | Yes | Yes | No |
| Redeclarable | Yes | No | No |

## 2. `let` - Block Scoped, Mutable Variables
The `let` keyword allows you to declare variables **that can be reassigned** but **cannot be redeclared in the same scope**.

### **Example of Block Scope**
```js
if (true) {
    let x = 10;
    console.log(x); // 10
}
console.log(x); // ReferenceError: x is not defined
```
Here, `x` is only available inside the `if` block.

### **Example of Reassignment**
```js
let name = "John";
name = "Doe";
console.log(name); // Doe
```
`let` allows reassignment but not redeclaration within the same scope:
```js
let age = 25;
let age = 30; // SyntaxError: Identifier 'age' has already been declared
```

## 3. `const` - Block Scoped, Immutable Variables
The `const` keyword is used for **variables that should not be reassigned**. However, **objects and arrays declared with `const` are mutable**.

### **Example of Constant Values**
```js
const pi = 3.1416;
pi = 3.14; // TypeError: Assignment to constant variable.
```

### **Mutable Objects with `const`**
```js
const person = { name: "Alice", age: 25 };
person.age = 26; // Allowed (modifying properties)
console.log(person); // { name: "Alice", age: 26 }
```
While the **object properties** can change, you **cannot reassign** the variable:
```js
person = {}; // TypeError: Assignment to constant variable.
```

## 4. Temporal Dead Zone (TDZ)
Variables declared with `let` and `const` **are hoisted** but remain **uninitialized** until their declaration.

### **Example of TDZ**
```js
console.log(a); // ReferenceError: Cannot access 'a' before initialization
let a = 5;
```
This happens because `a` is in the **Temporal Dead Zone** (TDZ) before its declaration.

## 5. Best Practices
- Use **`const` by default**. Only use `let` if reassignment is necessary.
- Avoid `var` as it leads to unpredictable behavior due to **hoisting** and **function scope**.
- Use **block scope** (`let` and `const`) to avoid variable leakage and accidental redeclarations.

## 6. Summary
- **`let`**: Block-scoped, can be reassigned but not redeclared.
- **`const`**: Block-scoped, cannot be reassigned, but mutable for objects and arrays.
- **TDZ** prevents accessing variables before declaration.
- **Use `const` by default**, unless reassignment is needed.

Understanding `let` and `const` helps write cleaner, more predictable JavaScript code!

