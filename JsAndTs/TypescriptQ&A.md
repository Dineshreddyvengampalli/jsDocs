# TypeScript Interview Questions and Answers

This document contains **frequently asked and tricky TypeScript interview questions** with detailed explanations and examples.

---
## 1. What are the key differences between TypeScript and JavaScript?
### **Answer:**
| Feature | TypeScript | JavaScript |
|---------|-----------|------------|
| Typing | Statically typed | Dynamically typed |
| Compilation | Compiles to JavaScript | No compilation needed |
| Interfaces | Supports interfaces | No built-in interface support |
| OOP Features | Supports classes, interfaces, generics | Limited OOP support |

### **Example:**
```ts
let name: string = "John";
// TypeScript enforces type safety, JavaScript does not.
```

---
## 2. What are TypeScript Interfaces and how are they used?
### **Answer:**
Interfaces define the structure of an object.
```ts
interface User {
    id: number;
    name: string;
    age?: number; // Optional property
}

const user: User = { id: 1, name: "Alice" };
```

---
## 3. What is the difference between `interface` and `type` in TypeScript?
### **Answer:**
| Feature | Interface | Type |
|---------|-----------|------|
| Extensibility | Can be extended | Cannot be extended |
| Use Case | Preferred for object shape | Used for complex types |

### **Example:**
```ts
interface Person {
    name: string;
}

type Animal = { species: string };
```

---
## 4. What are Generics in TypeScript?
### **Answer:**
Generics allow reusable code by making components work with different types.
```ts
function identity<T>(value: T): T {
    return value;
}

console.log(identity<string>("Hello"));
console.log(identity<number>(42));
```

---
## 5. What is Type Assertion in TypeScript?
### **Answer:**
Type assertions override TypeScript’s inferred type.
```ts
let value: any = "Hello";
let strLength: number = (value as string).length;
```

---
## 6. How do you achieve function overloading in TypeScript?
### **Answer:**
```ts
function add(a: number, b: number): number;
function add(a: string, b: string): string;
function add(a: any, b: any): any {
    return a + b;
}
```

---
## 7. What is the difference between `readonly` and `const`?
### **Answer:**
- `const` applies to variables.
- `readonly` applies to object properties.
```ts
const x = 10;
interface User { readonly id: number; }
```

---
## 8. What is the difference between `any`, `unknown`, and `never`?
### **Answer:**
| Type | Description |
|------|-------------|
| `any` | Allows any type (unsafe) |
| `unknown` | Safer than `any`, requires type checking |
| `never` | Represents values that never occur |

### **Example:**
```ts
let value: unknown;
if (typeof value === "string") {
    console.log(value.toUpperCase());
}
```

---
## 9. Explain the concept of `Partial<>`, `Required<>`, and `Readonly<>` utility types.
### **Answer:**
```ts
interface User {
    id: number;
    name: string;
}
let partialUser: Partial<User> = { id: 1 };
let readonlyUser: Readonly<User> = { id: 1, name: "Alice" };
```

---
## 10. What are Type Guards in TypeScript?
### **Answer:**
Type Guards narrow down types at runtime.
```ts
function isString(value: any): value is string {
    return typeof value === "string";
}
```

---
## 11. Explain `namespace` vs `module` in TypeScript.
### **Answer:**
- **Namespace**: Used for internal modularization.
- **Module**: Uses `import/export` syntax.

### **Example:**
```ts
namespace MyNamespace {
    export const value = 10;
}
console.log(MyNamespace.value);
```

```ts
export function greet(name: string) {
    return `Hello, ${name}`;
}
```

---
## 12. What is the difference between `abstract` class and `interface`?
### **Answer:**
| Feature | Abstract Class | Interface |
|---------|---------------|-----------|
| Methods | Can have implementations | Only method signatures |
| Inheritance | Single inheritance | Multiple inheritance |

### **Example:**
```ts
abstract class Animal {
    abstract makeSound(): void;
}

interface Person {
    name: string;
}
```

---
## 13. Explain Decorators in TypeScript.
### **Answer:**
Decorators are used in Angular and other frameworks for metadata.
```ts
function Logger(target: Function) {
    console.log(`Logging: ${target}`);
}
@Logger
class Car {}
```

---
## 14. What is `strictNullChecks` in TypeScript?
### **Answer:**
Enables strict checking for `null` and `undefined`.
```ts
let str: string | null = null;
```

---
## 15. Summary
- **Basic Types**: `number`, `string`, `boolean`, `any`, `unknown`
- **Functions**: Overloading, optional params
- **Interfaces & Classes**: Differences, inheritance
- **Generics**: Reusability
- **Utility Types**: `Partial<>`, `Readonly<>`
- **Type Guards & Decorators**: Advanced topics
