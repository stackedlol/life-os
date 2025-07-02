---
tags: language
---


> a programming language that adds interactivity to your website

### what is javascript
- Is a programming language that is one of the core technologies of the [[internet]]... alongside html and css. It allow us to add interactivity to pages via sliders, alerts, click interactions, popups, and etc on different websites.

- It also used in non-browser environments such as node.js for writing server-side code in javascript.

### foundational javascript concepts
- **"this" keyword**: refers to the context in which a function is executed. It provides a way to access the object that owns the code currently being executed. (hey, who's in charge here? depending on where code in running)

- prototypes

- **closure**: when you create a function inside another function, the inner function can "*remember*" the variables of the outer function... the memory is called closure (you PRESERVE data)

- async-style code

- **promise**: an object that represents a value that might not be available yet but will be resolved in the future. 

- **callback**: a #function you pass into another function to be *called later* when something happens. (when you are done, run this)

- timers
- observer pattern
- module pattern

### why javascript?
- browser built [[api]](s) built into web browsers, providing functionality such as dynamically creating html and setting css styles.

- third-party [[api]](s) that allow developers to incorporate functionality in sites from other content providers

- third-party [[framework]](s) and [[libraries]] that you can apply to html to accelerate building a user interface, enhancing [[user-experience]].


---
### javascript logic
all logic the the language is built on

1. **VARIABLES**
#variable: containers that store values. In javascript variables are denoted with the word "let" and the name of the variable. Variables are values needed to change in order to create a dynamic experience

- #string: this is a sequence of text denoted with `let MyVariable = "bob";`

- #number: a standard number value like `10`

- #boolean: a true/false statement like `true`

-  #array: structure that allows you to store multiple values in a single reference. 

- #object: this can be anything.. everything in javascript is an object and can be stored in a variable. 

2. **OPERATORS**
#operators are mathematical symbols that procedure a result based on two values (or variables)


3. **CONDITIONALS**
#conditionals: are code structures used to test if an expression returns true or not (if/else)

4. **FUNCTIONS**
#functions: are a way of packaging functionality that you wish to re-use

5. **EVENTS**
#events: code structure that listens for activity in the browser, and then runs code as a response.
```javascript
document.querySelector("html").addEventListener("click", () => {
  alert("Ouch! Stop poking me!");
});
```
In the example above, they added an `addEventListener` which is an anonymous function. It doesn't have a name and it sometimes associated with an arrow function.

---

### javascript data
