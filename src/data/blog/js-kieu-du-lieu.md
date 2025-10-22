---
title: "Kiểu dữ liệu trong JavaScript"
description: "Giới thiệu 8 kiểu dữ liệu cơ bản: string, number, boolean, null, undefined, object, symbol, bigint"
pubDate: 2025-01-02
category: "javascript"
draft: false
---

# Kiểu dữ liệu trong JavaScript

## Primitive Types (Kiểu nguyên thủy)

### 1. String (Chuỗi)
```javascript
const name = "John";
const message = 'Hello World';
const template = `Tên: ${name}`;
```

### 2. Number (Số)
```javascript
const age = 25;
const price = 99.99;
const infinity = Infinity;
const notANumber = NaN;
```

### 3. Boolean (Logic)
```javascript
const isActive = true;
const isCompleted = false;
```

### 4. Null
```javascript
const data = null; // Giá trị rỗng có chủ ý
```

### 5. Undefined
```javascript
let value; // undefined
const obj = {};
console.log(obj.name); // undefined
```

### 6. Symbol
```javascript
const id = Symbol('id');
const id2 = Symbol('id');
console.log(id === id2); // false
```

### 7. BigInt
```javascript
const bigNumber = 123456789012345678901234567890n;
const bigFromNumber = BigInt(123);
```

## Non-Primitive Type

### 8. Object
```javascript
const person = { name: "John", age: 25 };
const numbers = [1, 2, 3];
const fn = function() { return "Hello"; };
```

## Kiểm tra kiểu dữ liệu

```javascript
typeof "Hello"; // "string"
typeof 42; // "number"
typeof true; // "boolean"
typeof undefined; // "undefined"
typeof null; // "object" (đặc biệt)
typeof {}; // "object"
typeof []; // "object"
typeof function(){}; // "function"
```

## Chuyển đổi kiểu

```javascript
// Sang string
String(123); // "123"
(123).toString(); // "123"

// Sang number
Number("123"); // 123
+"123"; // 123
parseInt("123px"); // 123

// Sang boolean
Boolean(1); // true
!!1; // true
```