---
title: "Cách xử lý sự kiện (click, input, submit) trong JavaScript"
description: "Viết ví dụ thực hành: khi bấm nút đổi màu nền, hiện alert, v.v."
pubDate: 2025-01-10
category: "javascript"
draft: false
---

# Cách xử lý sự kiện (click, input, submit) trong JavaScript

## addEventListener cơ bản

```javascript
const button = document.querySelector("#my-button");

// Cách 1: addEventListener (khuyến nghị)
button.addEventListener("click", function() {
    console.log("Button clicked!");
});

// Cách 2: onclick property
button.onclick = function() {
    console.log("Button clicked!");
};

// Cách 3: inline HTML (không khuyến nghị)
// <button onclick="alert('Clicked!')">Click me</button>
```

## Click events - ví dụ thực tế

```html
<button id="color-btn">Đổi màu nền</button>
<button id="alert-btn">Hiện thông báo</button>
<button id="toggle-btn">Ẩn/hiện nội dung</button>
<div id="content">Nội dung có thể ẩn/hiện</div>
```

```javascript
// Đổi màu nền random
const colorBtn = document.querySelector("#color-btn");
colorBtn.addEventListener("click", () => {
    const colors = ["#ff6b6b", "#4ecdc4", "#45b7d1", "#96ceb4", "#ffeaa7"];
    const randomColor = colors[Math.floor(Math.random() * colors.length)];
    document.body.style.backgroundColor = randomColor;
});

// Hiện alert
const alertBtn = document.querySelector("#alert-btn");
alertBtn.addEventListener("click", () => {
    alert("Xin chào! Đây là thông báo từ JavaScript.");
});

// Toggle ẩn/hiện content
const toggleBtn = document.querySelector("#toggle-btn");
const content = document.querySelector("#content");
toggleBtn.addEventListener("click", () => {
    content.style.display = content.style.display === "none" ? "block" : "none";
});
```

## Input events

```html
<input type="text" id="search-input" placeholder="Tìm kiếm...">
<input type="range" id="font-size-slider" min="12" max="30" value="16">
<p id="demo-text">Văn bản demo để thay đổi kích thước</p>
```

```javascript
// Real-time search
const searchInput = document.querySelector("#search-input");
searchInput.addEventListener("input", (e) => {
    const searchTerm = e.target.value.toLowerCase();
    console.log("Đang tìm:", searchTerm);
    
    // Giả lập filter danh sách
    const items = document.querySelectorAll(".search-item");
    items.forEach(item => {
        const text = item.textContent.toLowerCase();
        item.style.display = text.includes(searchTerm) ? "block" : "none";
    });
});

// Thay đổi font size với slider
const fontSlider = document.querySelector("#font-size-slider");
const demoText = document.querySelector("#demo-text");

fontSlider.addEventListener("input", (e) => {
    const fontSize = e.target.value + "px";
    demoText.style.fontSize = fontSize;
});
```

## Form submit events

```html
<form id="user-form">
    <input type="text" id="username" placeholder="Tên đăng nhập" required>
    <input type="email" id="email" placeholder="Email" required>
    <input type="password" id="password" placeholder="Mật khẩu" required>
    <button type="submit">Đăng ký</button>
</form>
<div id="result"></div>
```

```javascript
const form = document.querySelector("#user-form");
const result = document.querySelector("#result");

form.addEventListener("submit", (e) => {
    e.preventDefault(); // Ngăn form submit mặc định
    
    // Lấy dữ liệu form
    const formData = new FormData(form);
    const username = document.querySelector("#username").value;
    const email = document.querySelector("#email").value;
    const password = document.querySelector("#password").value;
    
    // Validation đơn giản
    if (password.length < 6) {
        result.innerHTML = '<p style="color: red;">Mật khẩu phải có ít nhất 6 ký tự</p>';
        return;
    }
    
    // Thành công
    result.innerHTML = `
        <p style="color: green;">Đăng ký thành công!</p>
        <p>Tên: ${username}</p>
        <p>Email: ${email}</p>
    `;
    
    form.reset(); // Reset form
});
```

## Event object và properties

```javascript
document.addEventListener("click", (e) => {
    console.log("Event type:", e.type); // "click"
    console.log("Target element:", e.target); // element được click
    console.log("Mouse position:", e.clientX, e.clientY);
    console.log("Key pressed:", e.ctrlKey, e.shiftKey, e.altKey);
});

// Keyboard events
document.addEventListener("keydown", (e) => {
    console.log("Key pressed:", e.key);
    console.log("Key code:", e.keyCode);
    
    // Phím tắt Ctrl+S
    if (e.ctrlKey && e.key === "s") {
        e.preventDefault(); // Ngăn browser save page
        console.log("Save shortcut pressed!");
    }
});
```

## Event delegation

```html
<ul id="task-list">
    <li>Task 1 <button class="delete">Delete</button></li>
    <li>Task 2 <button class="delete">Delete</button></li>
    <li>Task 3 <button class="delete">Delete</button></li>
</ul>
<button id="add-task">Add New Task</button>
```

```javascript
const taskList = document.querySelector("#task-list");

// Event delegation - lắng nghe trên parent
taskList.addEventListener("click", (e) => {
    if (e.target.classList.contains("delete")) {
        e.target.parentElement.remove();
    }
});

// Thêm task mới
const addBtn = document.querySelector("#add-task");
let taskCount = 3;

addBtn.addEventListener("click", () => {
    taskCount++;
    const newTask = document.createElement("li");
    newTask.innerHTML = `Task ${taskCount} <button class="delete">Delete</button>`;
    taskList.appendChild(newTask);
});
```

## Multiple event types

```javascript
const input = document.querySelector("#multi-input");

// Nhiều event types cho cùng element
["focus", "blur", "input", "change"].forEach(eventType => {
    input.addEventListener(eventType, (e) => {
        console.log(`${eventType} event triggered`);
    });
});

// Hoặc cùng function cho nhiều events
function handleInputEvent(e) {
    console.log(`Input ${e.type}:`, e.target.value);
}

input.addEventListener("focus", handleInputEvent);
input.addEventListener("blur", handleInputEvent);
input.addEventListener("input", handleInputEvent);
```

## Remove event listeners

```javascript
const button = document.querySelector("#temp-button");

function handleClick() {
    console.log("Button clicked!");
    
    // Xóa event listener sau lần click đầu tiên
    button.removeEventListener("click", handleClick);
}

button.addEventListener("click", handleClick);

// Hoặc sử dụng { once: true }
button.addEventListener("click", () => {
    console.log("This will only run once");
}, { once: true });
```

## Practical example: Image gallery

```html
<div class="gallery">
    <img src="image1.jpg" alt="Image 1" class="gallery-img">
    <img src="image2.jpg" alt="Image 2" class="gallery-img">
    <img src="image3.jpg" alt="Image 3" class="gallery-img">
</div>
<div id="lightbox" class="lightbox" style="display: none;">
    <img id="lightbox-img" src="" alt="">
    <button id="close-lightbox">×</button>
</div>
```

```javascript
const gallery = document.querySelector(".gallery");
const lightbox = document.querySelector("#lightbox");
const lightboxImg = document.querySelector("#lightbox-img");
const closeBtn = document.querySelector("#close-lightbox");

// Click vào ảnh để phát to
gallery.addEventListener("click", (e) => {
    if (e.target.classList.contains("gallery-img")) {
        lightboxImg.src = e.target.src;
        lightbox.style.display = "flex";
    }
});

// Đóng lightbox
closeBtn.addEventListener("click", () => {
    lightbox.style.display = "none";
});

// ESC key để đóng
document.addEventListener("keydown", (e) => {
    if (e.key === "Escape" && lightbox.style.display === "flex") {
        lightbox.style.display = "none";
    }
});
```