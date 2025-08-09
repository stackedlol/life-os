---
tags: javascript
---

### what are closures?
- [[functions]] that remembers variables from the place it was created even after that outer function is done running

### why closures?
- creates custom, reusable logic (counters, settings, toggles)
- used in [[react]] hooks
- helpful in [[async]] code
- enables advanced patterns (currying, memorization, debounce)

### example...
```js
function createLikeButton() {
  let likes = 0; // private like count

  return function clickLike() {
    likes++;
    console.log(`👍 ${likes} likes`);
  };
}

// Make a new like button
const likePost = createLikeButton();

likePost(); // 👍 1 likes
likePost(); // 👍 2 likes
likePost(); // 👍 3 likes

```
