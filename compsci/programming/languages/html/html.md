---
tags: language
---

> HyperText Markup Language is used for #frontend development

### Why is html important?
- It gives the frontend of a website structure
- you can combing programming languages like [[css]] for styling and [[javascript]] to make the website interactive.

### foundational html concepts
1. [[semantics]] (universal structure tags) are commonly used to structure pages

2. **form control** is an element that enables user interaction and data entry or selection 

	- through *client-side* form validation, all required form controls are filled out in the correct format which helps ensure when that data is submitted, it matches the requirements set forth in the various form controls.

3. **event delegation**: is a technique where you attach a single event listener to a parent element instead of multiple listeners to each child element (used for performance)


4. **DOM traversal**: refers to navigating through the DOM tree to access or manipulate elements based on their relationships, like parent, child, or sibling nodes.  It's used to dynamically find and work with elements in a structured way without relying solely on selectors 


5. **DOM manipulation**: means using Javascript to change, add, or remove elements or content in the web page after it has loaded (allows for website to be dynamic without reloading the whole page)

### how is data handled in html?
- When a form is submitted (when a user hits a submit button), the browser makes a **request**. A script needs to respond to that request and process the data. The script is running on the *server* or *client*... It may validate the data, save it into a database, or do other operations based on the form data.

### how is data transferred in html?

- ==GET==: when you're asking for something from the server without effects, like retrieving a page. (requesting a webpage or fetching data from an API)

	- Mainly used if you want to retrieve data from the server without modifying it, not meant for modifying resources. Can be cached by browsers too.

- ==POST==: when you're sending information to the server that will result in some change like creating or updating data. (submitting a form, creating a new user account, or updating data on the server)

	- For forms that process sensitive data... use the POST method. (the data will not be visible in the URL can only be accessed from a frontend or backend script) This is where we utilized standardized [[protocols]] like #HTTPS to encrypt the data and make it only accessible via the backend-end script. (a common example of this would be a sign in form)

###








