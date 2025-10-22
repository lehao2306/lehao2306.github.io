---
title: "Vòng lặp trong JavaScript (for, while, for...of, for...in)"
description: "Giới thiệu và ví dụ từng loại vòng lặp, khi nào nên dùng loại nào"
pubDate: 2025-01-05
category: "javascript"
draft: false
---

# Vòng lặp trong JavaScript

## For loop - cơ bản

```javascript
// In số từ 1 đến 5
for (let i = 1; i <= 5; i++) {
    console.log(`Số: ${i}`);
}

// Lặp ngược
for (let i = 5; i >= 1; i--) {
    console.log(`Countdown: ${i}`);
}
```

## While loop

```javascript
let count = 0;
while (count < 3) {
    console.log(`Lần thứ: ${count + 1}`);
    count++;
}

// Ví dụ: Nhập số cho đến khi đúng
let number;
while (number !== 7) {
    number = Math.floor(Math.random() * 10) + 1;
    console.log(`Số random: ${number}`);
}
```

## Do...while loop

```javascript
let password;
do {
    password = prompt("Nhập mật khẩu:");
} while (password !== "123456");

console.log("Mật khẩu đúng!");
```

## For...of - lặp qua giá trị

```javascript
const fruits = ["táo", "cam", "chuối"];

// Lặp qua giá trị
for (const fruit of fruits) {
    console.log(`Tôi thích ${fruit}`);
}

// Với string
const text = "Hello";
for (const char of text) {
    console.log(char); // H, e, l, l, o
}
```

## For...in - lặp qua key/index

```javascript
const person = {
    name: "John",
    age: 25,
    city: "Hà Nội"
};

// Lặp qua thuộc tính object
for (const key in person) {
    console.log(`${key}: ${person[key]}`);
}

// Với array (không khuyến nghị)
const colors = ["red", "green", "blue"];
for (const index in colors) {
    console.log(`${index}: ${colors[index]}`);
}
```

## Khi nào dùng loại nào?

### For - khi biết số lần lặp
```javascript
// Tạo bảng cửu chương
for (let i = 1; i <= 9; i++) {
    console.log(`5 x ${i} = ${5 * i}`);
}
```

### While - khi không biết số lần lặp
```javascript
// Tìm số nguyên tố đầu tiên > 100
let num = 101;
while (!isPrime(num)) {
    num++;
}
console.log(`Số nguyên tố đầu tiên > 100: ${num}`);
```

### For...of - lặp qua giá trị (array, string, Set, Map)
```javascript
const numbers = [1, 2, 3, 4, 5];
const squares = [];

for (const num of numbers) {
    squares.push(num * num);
}
console.log(squares); // [1, 4, 9, 16, 25]
```

### For...in - lặp qua thuộc tính object
```javascript
function countProperties(obj) {
    let count = 0;
    for (const key in obj) {
        if (obj.hasOwnProperty(key)) {
            count++;
        }
    }
    return count;
}
```

## Break và Continue

```javascript
// Break - thoát khỏi vòng lặp
for (let i = 1; i <= 10; i++) {
    if (i === 5) break;
    console.log(i); // 1, 2, 3, 4
}

// Continue - bỏ qua lần lặp hiện tại
for (let i = 1; i <= 5; i++) {
    if (i === 3) continue;
    console.log(i); // 1, 2, 4, 5
}
```

## Nested loops

```javascript
// In bảng cửu chương
for (let i = 1; i <= 3; i++) {
    console.log(`Bảng cửu chương ${i}:`);
    for (let j = 1; j <= 5; j++) {
        console.log(`${i} x ${j} = ${i * j}`);
    }
    console.log("---");
}
```