---
tags: javascript
---


### functions and scope in javascript...
- functions: reusable blocks of code you can call
- scope: where a variable "lives" - and who can see it

### block scope vs function scope
- block scope: variable lives only inside {}
- function scope: variable lives inside the whole function

### example...
```js
function test() {
  if (true) {
    let a = 10;
    const b = 20;
    var c = 30;
  }

  console.log(a); // ❌ won't work
  console.log(b); // ❌ won't work
  console.log(c); // ✅ works (weird!)
}
```
