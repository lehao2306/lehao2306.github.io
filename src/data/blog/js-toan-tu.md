---
title: "Toán tử trong JavaScript"
description: "Giải thích các loại toán tử: số học, logic, so sánh, gán, typeof, instanceof"
pubDate: 2025-01-03
category: "javascript"
draft: false
---

# Toán tử trong JavaScript

## Toán tử số học

```javascript
const a = 10, b = 3;

console.log(a + b); // 13 - cộng
console.log(a - b); // 7 - trừ
console.log(a * b); // 30 - nhân
console.log(a / b); // 3.333... - chia
console.log(a % b); // 1 - chia lấy dư
console.log(a ** b); // 1000 - lũy thừa
```

## Toán tử gán

```javascript
let x = 5;
x += 3; // x = x + 3 → 8
x -= 2; // x = x - 2 → 6
x *= 2; // x = x * 2 → 12
x /= 4; // x = x / 4 → 3
x %= 2; // x = x % 2 → 1
x++; // x = x + 1 → 2
++x; // x = x + 1 → 3
x--; // x = x - 1 → 2
```

## Toán tử so sánh

```javascript
console.log(5 == "5"); // true - so sánh giá trị
console.log(5 === "5"); // false - so sánh cả kiểu
console.log(5 != "6"); // true
console.log(5 !== "5"); // true
console.log(10 > 5); // true
console.log(10 < 5); // false
console.log(10 >= 10); // true
console.log(5 <= 10); // true
```

## Toán tử logic

```javascript
const a = true, b = false;

console.log(a && b); // false - AND
console.log(a || b); // true - OR
console.log(!a); // false - NOT

// Short-circuit evaluation
const name = user && user.name; // Kiểm tra user tồn tại
const defaultName = name || "Guest"; // Giá trị mặc định
```

## Toán tử kiểm tra kiểu

```javascript
// typeof
console.log(typeof "hello"); // "string"
console.log(typeof 42); // "number"
console.log(typeof true); // "boolean"

// instanceof
const arr = [1, 2, 3];
console.log(arr instanceof Array); // true
console.log(arr instanceof Object); // true

const date = new Date();
console.log(date instanceof Date); // true
```

## Toán tử điều kiện (Ternary)

```javascript
const age = 18;
const status = age >= 18 ? "Adult" : "Minor";
console.log(status); // "Adult"

// Nhiều điều kiện
const grade = score >= 90 ? "A" : score >= 80 ? "B" : "C";
```

## Toán tử Nullish Coalescing

```javascript
const user = { name: null };
const displayName = user.name ?? "Anonymous";
console.log(displayName); // "Anonymous"

// So với ||
const value1 = 0 || "default"; // "default"
const value2 = 0 ?? "default"; // 0
```