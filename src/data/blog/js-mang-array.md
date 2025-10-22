---
title: "Làm việc với mảng (Array) trong JavaScript"
description: "Hướng dẫn các phương thức phổ biến: map, filter, reduce, forEach, find"
pubDate: 2025-01-07
category: "javascript"
draft: false
---

# Làm việc với mảng (Array) trong JavaScript

## Tạo mảng

```javascript
// Các cách tạo mảng
const fruits = ["táo", "cam", "chuối"];
const numbers = new Array(1, 2, 3, 4, 5);
const empty = [];
const mixed = [1, "hello", true, { name: "John" }];
```

## forEach - lặp qua từng phần tử

```javascript
const colors = ["đỏ", "xanh", "vàng"];

colors.forEach((color, index) => {
    console.log(`${index}: ${color}`);
});
// 0: đỏ
// 1: xanh  
// 2: vàng

// Practical example
const prices = [100, 200, 300];
let total = 0;
prices.forEach(price => total += price);
console.log(total); // 600
```

## map - tạo mảng mới từ mảng cũ

```javascript
const numbers = [1, 2, 3, 4, 5];

// Nhân đôi các số
const doubled = numbers.map(num => num * 2);
console.log(doubled); // [2, 4, 6, 8, 10]

// Tạo object từ array
const users = ["John", "Jane", "Bob"];
const userObjects = users.map((name, index) => ({
    id: index + 1,
    name: name,
    email: `${name.toLowerCase()}@email.com`
}));

console.log(userObjects);
// [
//   { id: 1, name: "John", email: "john@email.com" },
//   { id: 2, name: "Jane", email: "jane@email.com" },
//   { id: 3, name: "Bob", email: "bob@email.com" }
// ]
```

## filter - lọc phần tử

```javascript
const ages = [15, 18, 21, 17, 25, 30];

// Lọc tuổi >= 18
const adults = ages.filter(age => age >= 18);
console.log(adults); // [18, 21, 25, 30]

// Lọc số chẵn
const evenNumbers = [1, 2, 3, 4, 5, 6].filter(num => num % 2 === 0);
console.log(evenNumbers); // [2, 4, 6]

// Lọc object
const products = [
    { name: "Laptop", price: 1000, inStock: true },
    { name: "Mouse", price: 50, inStock: false },
    { name: "Keyboard", price: 100, inStock: true }
];

const availableProducts = products.filter(product => product.inStock);
console.log(availableProducts); // Laptop và Keyboard
```

## find - tìm phần tử đầu tiên

```javascript
const students = [
    { name: "An", grade: 85 },
    { name: "Bình", grade: 92 },
    { name: "Chi", grade: 78 }
];

// Tìm học sinh có điểm > 90
const topStudent = students.find(student => student.grade > 90);
console.log(topStudent); // { name: "Bình", grade: 92 }

// Tìm index
const topIndex = students.findIndex(student => student.grade > 90);
console.log(topIndex); // 1
```

## reduce - tính toán tổng hợp

```javascript
const numbers = [1, 2, 3, 4, 5];

// Tính tổng
const sum = numbers.reduce((acc, num) => acc + num, 0);
console.log(sum); // 15

// Tìm số lớn nhất
const max = numbers.reduce((acc, num) => Math.max(acc, num));
console.log(max); // 5

// Đếm số lần xuất hiện
const fruits = ["táo", "cam", "táo", "chuối", "cam", "táo"];
const count = fruits.reduce((acc, fruit) => {
    acc[fruit] = (acc[fruit] || 0) + 1;
    return acc;
}, {});
console.log(count); // { táo: 3, cam: 2, chuối: 1 }

// Group by
const people = [
    { name: "An", age: 25 },
    { name: "Bình", age: 30 },
    { name: "Chi", age: 25 }
];

const groupByAge = people.reduce((acc, person) => {
    const age = person.age;
    if (!acc[age]) acc[age] = [];
    acc[age].push(person);
    return acc;
}, {});
console.log(groupByAge);
```

## Các phương thức khác

```javascript
const numbers = [1, 2, 3, 4, 5];

// some - kiểm tra ít nhất 1 phần tử thỏa mãn
const hasEven = numbers.some(num => num % 2 === 0);
console.log(hasEven); // true

// every - kiểm tra tất cả phần tử thỏa mãn  
const allPositive = numbers.every(num => num > 0);
console.log(allPositive); // true

// includes - kiểm tra có chứa phần tử
console.log(numbers.includes(3)); // true

// sort - sắp xếp
const names = ["Charlie", "Alice", "Bob"];
names.sort(); // ["Alice", "Bob", "Charlie"]

const nums = [10, 5, 40, 25, 1000, 1];
nums.sort((a, b) => a - b); // [1, 5, 10, 25, 40, 1000]

// reverse - đảo ngược
const reversed = [1, 2, 3].reverse(); // [3, 2, 1]
```

## Chaining methods

```javascript
const products = [
    { name: "Laptop", price: 1000, category: "Electronics" },
    { name: "Shirt", price: 50, category: "Clothing" },
    { name: "Phone", price: 800, category: "Electronics" },
    { name: "Pants", price: 80, category: "Clothing" }
];

// Chain multiple methods
const expensiveElectronics = products
    .filter(product => product.category === "Electronics")
    .filter(product => product.price > 500)
    .map(product => product.name);

console.log(expensiveElectronics); // ["Laptop", "Phone"]
```