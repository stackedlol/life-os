---
tags: javascript
---

### what is the DOM?
- the Document Object Model (DOM) is how programs see *html* and *xml* documents... it lets script change the **page's structure** **content**, and **style** dynamically
- manipulated by [[javascript]]
- dynamic representation the browser updates in real-time

### core components of the DOM
- the DOM represents a logical tree
	- each node contains objects (head/body/etc from [[html]])
	- nodes can also have event handlers attached to them 

### functions of the DOM
- *querying element(s)*
	- find elements on the page to change and use
	- grab important parts of the UI like buttons, inputs, divs
- *DOM tree navigation*
	- real UI's are nested (cards inside lists)
- *modifying content*
	- UI needs to be updated based on actions or data
	- like changing text, updating links, replacing an image
- *styling elements*
	- UI needs to visually respond to state changes
- *creating or removing elements*
	- UI's are dynamic, you need to add/remove items like cards, modals, list items, etc
- *event handling & delegation*
	- UI's must respond to user interactions
- *forms and inputs*
	- all real apps need to collect user input

### example of the DOM

> a basic todo app built with [[html]], [[css]], and [[javascript]]


html for todo app
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Todo App</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>To-Do List</h1>

  <!-- #7: Input where user types a task -->
  <input id="taskInput" type="text" placeholder="Enter a task..." />

  <!-- #6: Button that triggers an event to add task -->
  <button id="addBtn">Add Task</button>

  <!-- #5: This is where we will add tasks dynamically -->
  <ul id="taskList"></ul>

  <script src="script.js"></script>
</body>
</html>

```

css for todo app
```css
body {
  font-family: sans-serif;
  max-width: 400px;
  margin: 40px auto;
  padding: 1rem;
  background-color: #f8f8f8;
  border-radius: 10px;
}

input {
  width: 70%;
  padding: 0.5rem;
  margin-bottom: 1rem;
}

button {
  padding: 0.5rem;
  margin-left: 0.5rem;
  cursor: pointer;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  padding: 0.5rem;
  margin-top: 0.5rem;
  background: white;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border: 1px solid #ddd;
  border-radius: 5px;
}

li.done {
  text-decoration: line-through;
  color: gray;
}
```

js for todo app
```js
/// =====================================
// ✅ #1 QUERYING ELEMENTS
// These let you "grab" parts of the DOM to work with them in JS
const input = document.getElementById("taskInput");       // #1
const button = document.getElementById("addBtn");         // #1
const taskList = document.getElementById("taskList");     // #1

// =====================================
// ✅ #6 EVENT HANDLING
// Trigger a function when the "Add Task" button is clicked
button.addEventListener("click", () => {                  // #6

  // ✅ #7 FORMS & INPUTS
  // Grab what the user typed into the input field
  const taskText = input.value.trim();                    // #7

  if (taskText !== "") {
    // =====================================
    // ✅ #5 CREATING DOM ELEMENTS
    // Build a new <li> item dynamically based on user input
    const li = document.createElement("li");              // #5

    // ✅ #3 MODIFYING CONTENT
    // Insert the user's task text inside the <li>
    li.innerText = taskText;                              // #3

    // =====================================
    // ✅ #4 STYLING ELEMENTS
    // Toggle a CSS class when the task is clicked (for strikethrough)
    li.addEventListener("click", () => {                  // #6
      li.classList.toggle("done");                        // #4
    });

    // =====================================
    // ✅ #5 CREATING DOM ELEMENTS (continued)
    // Build a delete button and add it to the task <li>
    const deleteBtn = document.createElement("button");   // #5
    deleteBtn.innerText = "❌";                           // #3
    deleteBtn.style.marginLeft = "10px";                  // #4

    // ✅ #6 EVENT HANDLING (Delete Button)
    deleteBtn.addEventListener("click", (e) => {          // #6
      e.stopPropagation(); // Prevents li click from firing
      li.remove();         // ✅ #5 REMOVING DOM ELEMENTS
    });

    // =====================================
    // ✅ #2 DOM TREE NAVIGATION
    // Attach the delete button to the <li>
    li.appendChild(deleteBtn);                            // #2

    // ✅ #2 DOM TREE NAVIGATION
    // Add the completed <li> (with deleteBtn inside) to the <ul>
    taskList.appendChild(li);                             // #2

    // =====================================
    // ✅ #7 FORMS & INPUTS (clearing input)
    input.value = "";                                     // #7
  }
});

```


