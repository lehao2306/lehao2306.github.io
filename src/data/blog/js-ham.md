---
title: "Hàm trong JavaScript – cách khai báo và gọi hàm"
description: "Giải thích function declaration, function expression, arrow function"
pubDate: 2025-01-06
category: "javascript"
draft: false
---

# Hàm trong JavaScript

## Function Declaration

```javascript
function sayHello(name) {
    return `Xin chào, ${name}!`;
}

// Gọi hàm
console.log(sayHello("An")); // "Xin chào, An!"

// Hoisting - có thể gọi trước khi khai báo
greet(); // "Hello World!"

function greet() {
    console.log("Hello World!");
}
```

## Function Expression

```javascript
const add = function(a, b) {
    return a + b;
};

console.log(add(5, 3)); // 8

// Không có hoisting
// subtract(5, 3); // ❌ Error: Cannot access before initialization

const subtract = function(a, b) {
    return a - b;
};
```

## Arrow Function

```javascript
// Cú pháp cơ bản
const multiply = (a, b) => {
    return a * b;
};

// Rút gọn (một dòng)
const square = x => x * x;
const double = x => x * 2;

// Không có tham số
const getCurrentTime = () => new Date().toLocaleTimeString();

// Một tham số (không cần dấu ngoặc)
const isEven = num => num % 2 === 0;

console.log(square(5)); // 25
console.log(isEven(4)); // true
```

## Parameters và Arguments

```javascript
// Default parameters
function createUser(name = "Guest", age = 0) {
    return { name, age };
}

console.log(createUser()); // { name: "Guest", age: 0 }
console.log(createUser("John", 25)); // { name: "John", age: 25 }

// Rest parameters
function sum(...numbers) {
    return numbers.reduce((total, num) => total + num, 0);
}

console.log(sum(1, 2, 3, 4)); // 10

// Destructuring parameters
function displayUser({ name, age, email }) {
    console.log(`Tên: ${name}, Tuổi: ${age}, Email: ${email}`);
}

displayUser({ name: "John", age: 25, email: "john@email.com" });
```

## Scope và Closure

```javascript
function outerFunction(x) {
    // Outer scope
    
    function innerFunction(y) {
        // Inner scope - có thể truy cập x
        return x + y;
    }
    
    return innerFunction;
}

const addFive = outerFunction(5);
console.log(addFive(3)); // 8

// Practical example: Counter
function createCounter() {
    let count = 0;
    
    return {
        increment: () => ++count,
        decrement: () => --count,
        getValue: () => count
    };
}

const counter = createCounter();
console.log(counter.increment()); // 1
console.log(counter.increment()); // 2
console.log(counter.getValue()); // 2
```

## Callback Functions

```javascript
function processArray(arr, callback) {
    const result = [];
    for (const item of arr) {
        result.push(callback(item));
    }
    return result;
}

const numbers = [1, 2, 3, 4, 5];

// Sử dụng với function expression
const doubled = processArray(numbers, function(x) {
    return x * 2;
});

// Sử dụng với arrow function
const squared = processArray(numbers, x => x * x);

console.log(doubled); // [2, 4, 6, 8, 10]
console.log(squared); // [1, 4, 9, 16, 25]
```

## Higher-Order Functions

```javascript
// Hàm trả về hàm khác
function multiplier(factor) {
    return function(number) {
        return number * factor;
    };
}

const double = multiplier(2);
const triple = multiplier(3);

console.log(double(5)); // 10
console.log(triple(4)); // 12

// Hàm nhận hàm khác làm tham số
function calculator(operation) {
    return function(a, b) {
        return operation(a, b);
    };
}

const add = calculator((a, b) => a + b);
const subtract = calculator((a, b) => a - b);

console.log(add(10, 5)); // 15
console.log(subtract(10, 5)); // 5
```

## Immediately Invoked Function Expression (IIFE)

```javascript
// IIFE - thực thi ngay lập tức
(function() {
    console.log("IIFE executed!");
})();

// Với parameters
(function(name) {
    console.log(`Hello, ${name}!`);
})("World");

// Arrow function IIFE
(() => {
    console.log("Arrow IIFE!");
})();
```