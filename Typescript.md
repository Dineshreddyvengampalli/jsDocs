# TypeScript Important Topics and Examples

This document covers **key TypeScript concepts** with examples to help you understand its features and best practices.

---
## 1. Introduction to TypeScript
### **What is TypeScript?**
TypeScript is a **statically typed superset** of JavaScript that compiles to plain JavaScript. It provides:
- **Static typing**
- **Interfaces and type safety**
- **Better tooling and autocompletion**

### **Installing TypeScript**
```bash
npm install -g typescript
```

Compile a TypeScript file:
```bash
tsc filename.ts
```

---
## 2. Basic Types
TypeScript introduces static types for better type safety.

```ts
let id: number = 5;
let name: string = "John";
let isActive: boolean = true;
let data: any = "Can be anything";
```

### **Arrays and Tuples**
```ts
let numbers: number[] = [1, 2, 3];
let tuple: [string, number] = ["Alice", 25];
```

### **Union Types**
```ts
let value: string | number;
value = "Hello"; // Valid
value = 10;      // Valid
```

---
## 3. Functions in TypeScript

### **Function with Type Annotations**
```ts
function add(a: number, b: number): number {
    return a + b;
}
```

### **Optional and Default Parameters**
```ts
function greet(name: string, age?: number) {
    return `Hello, ${name}${age ? `, age ${age}` : ''}`;
}
```

### **Arrow Functions**
```ts
const multiply = (a: number, b: number): number => a * b;
```

---
## 4. Interfaces
Interfaces define object structure and ensure type safety.

```ts
interface User {
    id: number;
    name: string;
    age?: number; // Optional property
}

const user: User = {
    id: 1,
    name: "Alice",
};
```

### **Interface with Functions**
```ts
interface MathOp {
    (a: number, b: number): number;
}

const add: MathOp = (a, b) => a + b;
```

---
## 5. Classes in TypeScript
TypeScript supports object-oriented programming with classes.

```ts
class Person {
    private id: number;
    public name: string;

    constructor(id: number, name: string) {
        this.id = id;
        this.name = name;
    }
}

const john = new Person(1, "John Doe");
```

### **Inheritance**
```ts
class Employee extends Person {
    role: string;

    constructor(id: number, name: string, role: string) {
        super(id, name);
        this.role = role;
    }
}
```

---
## 6. Generics
Generics allow flexible and reusable components.

```ts
function identity<T>(value: T): T {
    return value;
}
console.log(identity<string>("Hello"));
console.log(identity<number>(42));
```

### **Generic Interfaces**
```ts
interface Box<T> {
    value: T;
}

const box: Box<number> = { value: 100 };
```

---
## 7. Type Assertions
Convert one type to another.

```ts
let someValue: any = "Hello, TypeScript";
let strLength: number = (someValue as string).length;
```

---
## 8. Enums
Enums define named constants.

```ts
enum Color {
    Red,
    Green,
    Blue,
}
let myColor: Color = Color.Green;
```

---
## 9. Modules and Namespaces
TypeScript supports modularity with **ES Modules**.

### **Exporting a Module**
```ts
export function greet(name: string) {
    return `Hello, ${name}`;
}
```

### **Importing a Module**
```ts
import { greet } from "./module";
console.log(greet("Alice"));
```

---
## 10. Utility Types
TypeScript provides utility types for modifying existing types.

### **Partial** (Makes properties optional)
```ts
interface User {
    id: number;
    name: string;
}
let partialUser: Partial<User> = { id: 1 };
```

### **Readonly** (Prevents modification)
```ts
const user: Readonly<User> = { id: 1, name: "Alice" };
// user.id = 2; // Error
```

---
## 11. Advanced Topics

### **Type Guards** (Narrowing down types at runtime)
```ts
function isString(value: any): value is string {
    return typeof value === "string";
}
```

### **Decorators** (Used in frameworks like Angular)
```ts
function Logger(target: Function) {
    console.log(`Logging class: ${target}`);
}

@Logger
class Car {
    constructor(public brand: string) {}
}
```

---
## 12. Summary
- **Basic Types**: `number`, `string`, `boolean`, `any`, `union`
- **Functions**: Optional params, arrow functions, return types
- **Interfaces & Classes**: Object structure, inheritance
- **Generics**: Reusable components
- **Enums & Modules**: Code organization
- **Utility Types**: `Partial<>`, `Readonly<>`
- **Advanced Features**: Type guards, decorators
