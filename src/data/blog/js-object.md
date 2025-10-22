---
title: "Làm việc với đối tượng (Object) trong JavaScript"
description: "Cách tạo, truy cập, thêm/xóa thuộc tính, vòng lặp object"
pubDate: 2025-01-08
category: "javascript"
draft: false
---

# Làm việc với đối tượng (Object) trong JavaScript

## Tạo object

```javascript
// Object literal
const person = {
    name: "John",
    age: 25,
    city: "Hà Nội"
};

// Constructor function
function Car(brand, model, year) {
    this.brand = brand;
    this.model = model;
    this.year = year;
}

const myCar = new Car("Toyota", "Camry", 2023);

// Object.create()
const animal = {
    type: "Mammal",
    sound: function() {
        console.log("Making sound...");
    }
};

const dog = Object.create(animal);
dog.breed = "Golden Retriever";
```

## Truy cập thuộc tính

```javascript
const user = {
    firstName: "John",
    lastName: "Doe",
    age: 30,
    "full-name": "John Doe" // key có dấu gạch ngang
};

// Dot notation
console.log(user.firstName); // "John"
console.log(user.age); // 30

// Bracket notation
console.log(user["lastName"]); // "Doe"
console.log(user["full-name"]); // "John Doe"

// Dynamic access
const prop = "age";
console.log(user[prop]); // 30
```

## Thêm và sửa thuộc tính

```javascript
const student = {
    name: "An",
    age: 20
};

// Thêm thuộc tính mới
student.grade = "A";
student["email"] = "an@email.com";

// Sửa thuộc tính
student.age = 21;
student["name"] = "An Nguyen";

console.log(student);
// { name: "An Nguyen", age: 21, grade: "A", email: "an@email.com" }
```

## Xóa thuộc tính

```javascript
const product = {
    name: "Laptop",
    price: 1000,
    discount: 10,
    temp: "to be deleted"
};

// Xóa thuộc tính
delete product.temp;
delete product["discount"];

console.log(product); // { name: "Laptop", price: 1000 }

// Kiểm tra thuộc tính tồn tại
console.log("price" in product); // true
console.log("discount" in product); // false
console.log(product.hasOwnProperty("name")); // true
```

## Methods trong object

```javascript
const calculator = {
    result: 0,
    
    add: function(num) {
        this.result += num;
        return this; // cho phép chaining
    },
    
    multiply(num) { // ES6 shorthand syntax
        this.result *= num;
        return this;
    },
    
    // Arrow function không có 'this'
    reset: () => {
        // this.result = 0; // ❌ Không hoạt động
        calculator.result = 0; // ✅ Phải reference trực tiếp
    },
    
    getValue() {
        return this.result;
    }
};

// Method chaining
calculator.add(5).multiply(3).add(2);
console.log(calculator.getValue()); // 17
```

## Lặp qua object

```javascript
const book = {
    title: "JavaScript Guide",
    author: "John Doe",
    pages: 300,
    published: 2023
};

// For...in loop
for (const key in book) {
    console.log(`${key}: ${book[key]}`);
}

// Object.keys()
Object.keys(book).forEach(key => {
    console.log(`${key}: ${book[key]}`);
});

// Object.values()
Object.values(book).forEach(value => {
    console.log(value);
});

// Object.entries()
Object.entries(book).forEach(([key, value]) => {
    console.log(`${key}: ${value}`);
});
```

## Destructuring

```javascript
const user = {
    name: "Alice",
    age: 28,
    email: "alice@email.com",
    address: {
        city: "Hà Nội",
        district: "Cầu Giấy"
    }
};

// Basic destructuring
const { name, age } = user;
console.log(name, age); // "Alice" 28

// Rename variables
const { name: userName, email: userEmail } = user;
console.log(userName, userEmail); // "Alice" "alice@email.com"

// Default values
const { phone = "N/A" } = user;
console.log(phone); // "N/A"

// Nested destructuring
const { address: { city, district } } = user;
console.log(city, district); // "Hà Nội" "Cầu Giấy"
```

## Object methods hữu ích

```javascript
const original = { a: 1, b: 2 };
const source = { b: 3, c: 4 };

// Object.assign() - copy/merge objects
const merged = Object.assign({}, original, source);
console.log(merged); // { a: 1, b: 3, c: 4 }

// Spread operator (ES6)
const spreadMerged = { ...original, ...source };
console.log(spreadMerged); // { a: 1, b: 3, c: 4 }

// Object.freeze() - không thể thay đổi
const frozen = Object.freeze({ name: "John" });
// frozen.name = "Jane"; // ❌ Không có tác dụng

// Object.seal() - không thể thêm/xóa thuộc tính
const sealed = Object.seal({ name: "John", age: 25 });
sealed.age = 30; // ✅ OK - sửa được
// sealed.email = "john@email.com"; // ❌ Không thêm được
```

## JSON operations

```javascript
const person = {
    name: "John",
    age: 30,
    hobbies: ["reading", "gaming"]
};

// Object to JSON string
const jsonString = JSON.stringify(person);
console.log(jsonString); // '{"name":"John","age":30,"hobbies":["reading","gaming"]}'

// JSON string to Object
const parsedObject = JSON.parse(jsonString);
console.log(parsedObject); // { name: "John", age: 30, hobbies: ["reading", "gaming"] }

// Deep copy using JSON (có hạn chế)
const deepCopy = JSON.parse(JSON.stringify(person));
```