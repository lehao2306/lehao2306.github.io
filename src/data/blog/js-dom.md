---
title: "DOM là gì? Cách truy cập và thay đổi nội dung HTML bằng JavaScript"
description: "Giải thích DOM, ví dụ document.querySelector, innerHTML, addEventListener"
pubDate: 2025-01-09
category: "javascript"
draft: false
---

# DOM là gì? Cách truy cập và thay đổi nội dung HTML bằng JavaScript

## DOM là gì?

DOM (Document Object Model) là cây cấu trúc biểu diễn HTML document. JavaScript có thể thay đổi HTML thông qua DOM.

```html
<!DOCTYPE html>
<html>
<head>
    <title>My Page</title>
</head>
<body>
    <h1 id="title">Hello World</h1>
    <p class="text">This is a paragraph.</p>
    <button id="btn">Click me</button>
</body>
</html>
```

## Truy cập elements

```javascript
// Theo ID
const title = document.getElementById("title");
const button = document.getElementById("btn");

// Theo class name
const textElements = document.getElementsByClassName("text");
const firstText = textElements[0];

// Theo tag name
const allParagraphs = document.getElementsByTagName("p");

// Query selector (CSS selector)
const titleByQuery = document.querySelector("#title");
const textByQuery = document.querySelector(".text");
const firstButton = document.querySelector("button");

// Query selector all
const allTexts = document.querySelectorAll(".text");
const allButtons = document.querySelectorAll("button");
```

## Thay đổi nội dung

```javascript
// innerHTML - thay đổi HTML content
const title = document.querySelector("#title");
title.innerHTML = "<em>New Title with HTML</em>";

// textContent - chỉ text, không HTML
title.textContent = "Plain Text Title";

// innerText - text hiển thị (không bao gồm hidden elements)
title.innerText = "Visible Text Only";

// Ví dụ thực tế: Cập nhật thời gian
function updateTime() {
    const timeElement = document.querySelector("#current-time");
    timeElement.textContent = new Date().toLocaleTimeString();
}

setInterval(updateTime, 1000);
```

## Thay đổi attributes

```javascript
const image = document.querySelector("img");
const link = document.querySelector("a");

// Thay đổi src của image
image.src = "new-image.jpg";
image.alt = "New image description";

// Thay đổi href của link
link.href = "https://example.com";
link.target = "_blank";

// setAttribute và getAttribute
image.setAttribute("data-id", "123");
const dataId = image.getAttribute("data-id");

// Xóa attribute
image.removeAttribute("data-id");
```

## Thay đổi CSS styles

```javascript
const box = document.querySelector(".box");

// Thay đổi style trực tiếp
box.style.backgroundColor = "red";
box.style.width = "200px";
box.style.height = "100px";
box.style.fontSize = "16px";

// Thêm/xóa CSS classes
box.classList.add("active");
box.classList.remove("inactive");
box.classList.toggle("hidden"); // thêm nếu chưa có, xóa nếu đã có

// Kiểm tra class
if (box.classList.contains("active")) {
    console.log("Box is active");
}
```

## Tạo và thêm elements

```javascript
// Tạo element mới
const newParagraph = document.createElement("p");
newParagraph.textContent = "This is a new paragraph";
newParagraph.className = "new-text";

// Thêm vào DOM
const container = document.querySelector(".container");
container.appendChild(newParagraph);

// insertBefore
const existingElement = document.querySelector("#existing");
container.insertBefore(newParagraph, existingElement);

// innerHTML (cách khác)
container.innerHTML += "<p>Another new paragraph</p>";
```

## Xóa elements

```javascript
const elementToRemove = document.querySelector("#remove-me");

// Cách 1: remove() (ES6)
elementToRemove.remove();

// Cách 2: removeChild() (cũ)
const parent = elementToRemove.parentNode;
parent.removeChild(elementToRemove);

// Xóa tất cả children
const container = document.querySelector(".container");
container.innerHTML = ""; // Xóa tất cả
```

## Traversing DOM

```javascript
const element = document.querySelector("#middle");

// Parent elements
const parent = element.parentNode;
const parentElement = element.parentElement;

// Children elements
const children = element.children; // HTMLCollection
const firstChild = element.firstElementChild;
const lastChild = element.lastElementChild;

// Siblings
const nextSibling = element.nextElementSibling;
const previousSibling = element.previousElementSibling;

// Tìm element gần nhất theo selector
const closestContainer = element.closest(".container");
```

## Ví dụ thực tế: Todo List

```html
<div class="todo-app">
    <input type="text" id="todo-input" placeholder="Enter todo...">
    <button id="add-btn">Add Todo</button>
    <ul id="todo-list"></ul>
</div>
```

```javascript
const input = document.querySelector("#todo-input");
const addBtn = document.querySelector("#add-btn");
const todoList = document.querySelector("#todo-list");

function addTodo() {
    const todoText = input.value.trim();
    
    if (todoText === "") return;
    
    // Tạo li element
    const li = document.createElement("li");
    li.innerHTML = `
        <span>${todoText}</span>
        <button class="delete-btn">Delete</button>
    `;
    
    // Thêm event listener cho nút delete
    const deleteBtn = li.querySelector(".delete-btn");
    deleteBtn.addEventListener("click", () => {
        li.remove();
    });
    
    // Thêm vào list
    todoList.appendChild(li);
    
    // Clear input
    input.value = "";
}

addBtn.addEventListener("click", addTodo);

// Enter key để add todo
input.addEventListener("keypress", (e) => {
    if (e.key === "Enter") {
        addTodo();
    }
});
```

## Form handling

```javascript
const form = document.querySelector("#contact-form");
const nameInput = document.querySelector("#name");
const emailInput = document.querySelector("#email");

form.addEventListener("submit", (e) => {
    e.preventDefault(); // Ngăn form submit mặc định
    
    const name = nameInput.value;
    const email = emailInput.value;
    
    // Validation
    if (!name || !email) {
        alert("Please fill all fields");
        return;
    }
    
    // Process form data
    console.log("Form data:", { name, email });
    
    // Reset form
    form.reset();
});
```