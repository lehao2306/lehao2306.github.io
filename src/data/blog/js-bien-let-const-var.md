---
title: "Biến trong JavaScript: let, const và var khác nhau thế nào?"
description: "Giải thích cách khai báo biến và sự khác biệt giữa var, let, const trong JavaScript"
pubDate: 2025-01-01
category: "javascript"
draft: false
---

# Biến trong JavaScript: let, const và var

## Cách khai báo biến

### var
```javascript
var name = "John";
var age = 25;
var age = 30; // có thể khai báo lại
```

### let 
```javascript
let name = "John";
let age = 25;
age = 30; // có thể thay đổi giá trị
// let age = 35; // ❌ Lỗi: không thể khai báo lại
```

### const
```javascript
const name = "John";
// name = "Jane"; // ❌ Lỗi: không thể thay đổi
const person = { name: "John" };
person.name = "Jane"; // ✅ OK: có thể thay đổi thuộc tính
```

## Sự khác biệt chính

| | var | let | const |
|---|---|---|---|
| **Scope** | Function/Global | Block | Block |
| **Hoisting** | Có | Có (TDZ) | Có (TDZ) |
| **Re-declare** | ✅ | ❌ | ❌ |
| **Re-assign** | ✅ | ✅ | ❌ |

## Ví dụ thực tế

```javascript
// Block scope
if (true) {
    var varVariable = "var";
    let letVariable = "let";
    const constVariable = "const";
}

console.log(varVariable); // "var" - truy cập được
// console.log(letVariable); // ❌ Lỗi
// console.log(constVariable); // ❌ Lỗi
```

**Khuyến nghị:** Sử dụng `const` trước, `let` khi cần thay đổi giá trị, tránh `var`.