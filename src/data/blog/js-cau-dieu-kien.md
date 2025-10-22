---
title: "Câu điều kiện if...else và switch"
description: "Hướng dẫn cách viết điều kiện, ví dụ thực tế kiểm tra tuổi, điểm, đăng nhập"
pubDate: 2025-01-04
category: "javascript"
draft: false
---

# Câu điều kiện if...else và switch

## If...else cơ bản

```javascript
const age = 18;

if (age >= 18) {
    console.log("Bạn đủ tuổi bầu cử");
} else {
    console.log("Bạn chưa đủ tuổi");
}
```

## Else if - nhiều điều kiện

```javascript
const score = 85;

if (score >= 90) {
    console.log("Loại A - Xuất sắc");
} else if (score >= 80) {
    console.log("Loại B - Giỏi");
} else if (score >= 70) {
    console.log("Loại C - Khá");
} else if (score >= 50) {
    console.log("Loại D - Trung bình");
} else {
    console.log("Loại F - Yếu");
}
```

## Switch statement

```javascript
const day = "monday";

switch (day.toLowerCase()) {
    case "monday":
        console.log("Thứ hai - Bắt đầu tuần mới!");
        break;
    case "tuesday":
        console.log("Thứ ba");
        break;
    case "wednesday":
        console.log("Thứ tư");
        break;
    case "saturday":
    case "sunday":
        console.log("Cuối tuần - Nghỉ ngơi!");
        break;
    default:
        console.log("Ngày không hợp lệ");
}
```

## Ví dụ thực tế: Hệ thống đăng nhập

```javascript
function checkLogin(username, password) {
    if (!username || !password) {
        return "Vui lòng nhập đầy đủ thông tin";
    }
    
    if (username === "admin" && password === "123456") {
        return "Đăng nhập thành công";
    } else {
        return "Tài khoản hoặc mật khẩu không đúng";
    }
}

console.log(checkLogin("admin", "123456")); // "Đăng nhập thành công"
console.log(checkLogin("user", "wrong")); // "Tài khoản hoặc mật khẩu không đúng"
```

## Ví dụ: Tính phí shipping

```javascript
function calculateShipping(weight, distance) {
    let fee = 0;
    
    // Phí theo trọng lượng
    if (weight <= 1) {
        fee += 15000;
    } else if (weight <= 5) {
        fee += 25000;
    } else {
        fee += 40000;
    }
    
    // Phí theo khoảng cách
    if (distance > 100) {
        fee += 10000;
    }
    
    return fee;
}

console.log(calculateShipping(2, 150)); // 35000
```

## Ví dụ: Xác định mùa trong năm

```javascript
function getSeason(month) {
    switch (month) {
        case 12:
        case 1:
        case 2:
            return "Mùa đông";
        case 3:
        case 4:
        case 5:
            return "Mùa xuân";
        case 6:
        case 7:
        case 8:
            return "Mùa hè";
        case 9:
        case 10:
        case 11:
            return "Mùa thu";
        default:
            return "Tháng không hợp lệ";
    }
}

console.log(getSeason(6)); // "Mùa hè"
```

## Conditional (Ternary) Operator

```javascript
const age = 20;
const message = age >= 18 ? "Người lớn" : "Trẻ em";

// Nested ternary
const grade = score >= 90 ? "A" : score >= 80 ? "B" : score >= 70 ? "C" : "F";
```