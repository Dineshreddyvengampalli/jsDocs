# Understanding `map()`, `filter()`, and `reduce()` in JavaScript

JavaScript provides powerful higher-order functions like **`map()`**, **`filter()`**, and **`reduce()`** for working with arrays. These functions make it easier to process and transform data efficiently.

---
## 1. `map()` – Transforming an Array
The `map()` method creates a **new array** by applying a function to each element in the original array.

### **Syntax:**
```js
array.map(callbackFunction(element, index, array))
```

### **Example: Doubling Numbers**
```js
const numbers = [1, 2, 3, 4];
const doubled = numbers.map(num => num * 2);
console.log(doubled); // [2, 4, 6, 8]
```

### **Example: Extracting Values from an Array of Objects**
```js
const users = [
    { name: "Alice", age: 25 },
    { name: "Bob", age: 30 },
    { name: "Charlie", age: 35 }
];

const names = users.map(user => user.name);
console.log(names); // ["Alice", "Bob", "Charlie"]
```

---
## 2. `filter()` – Filtering an Array
The `filter()` method **creates a new array** with elements that satisfy a given condition.

### **Syntax:**
```js
array.filter(callbackFunction(element, index, array))
```

### **Example: Filtering Even Numbers**
```js
const numbers = [1, 2, 3, 4, 5, 6];
const evens = numbers.filter(num => num % 2 === 0);
console.log(evens); // [2, 4, 6]
```

### **Example: Filtering Users Above 30**
```js
const users = [
    { name: "Alice", age: 25 },
    { name: "Bob", age: 30 },
    { name: "Charlie", age: 35 }
];

const olderUsers = users.filter(user => user.age > 30);
console.log(olderUsers);
// [{ name: "Charlie", age: 35 }]
```

---
## 3. `reduce()` – Accumulating Values
The `reduce()` method **reduces an array to a single value** (e.g., sum, product, concatenation).

### **Syntax:**
```js
array.reduce(callbackFunction(accumulator, element, index, array), initialValue)
```

### **Example: Summing Numbers**
```js
const numbers = [1, 2, 3, 4];
const sum = numbers.reduce((acc, num) => acc + num, 0);
console.log(sum); // 10
```

### **Example: Counting Occurrences**
```js
const fruits = ["apple", "banana", "apple", "orange", "banana", "apple"];
const fruitCount = fruits.reduce((acc, fruit) => {
    acc[fruit] = (acc[fruit] || 0) + 1;
    return acc;
}, {});
console.log(fruitCount);
// { apple: 3, banana: 2, orange: 1 }
```

### **Example: Flattening an Array**
```js
const nestedArray = [[1, 2], [3, 4], [5, 6]];
const flatArray = nestedArray.reduce((acc, curr) => acc.concat(curr), []);
console.log(flatArray); // [1, 2, 3, 4, 5, 6]
```

---
## 4. Combining `map()`, `filter()`, and `reduce()`
These functions can be combined for powerful data manipulation.

### **Example: Sum of Squares of Even Numbers**
```js
const numbers = [1, 2, 3, 4, 5, 6];
const sumOfSquares = numbers
    .filter(num => num % 2 === 0) // [2, 4, 6]
    .map(num => num * num) // [4, 16, 36]
    .reduce((sum, num) => sum + num, 0); // 56

console.log(sumOfSquares); // 56
```

---
## 5. Summary
| Method  | Purpose |
|---------|---------|
| **`map()`**  | Transforms each element and returns a new array |
| **`filter()`** | Filters elements based on a condition |
| **`reduce()`** | Accumulates values into a single result |

- **Use `map()`** when transforming array elements.
- **Use `filter()`** when selecting specific elements.
- **Use `reduce()`** when combining array elements into one result.
