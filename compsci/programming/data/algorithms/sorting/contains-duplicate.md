---
tags: algorithms
---


> given an array integers, find if the array contains any duplicates

### Practical applications of this algorithm
- DATA VALIDATION: Sometimes data sets need to contain **unique** elements (no repeats). An example of this would be sorting through emails and usernames
### Type of algorithm:
- the "contains-duplicate" algorithm is an example of a #sorting algorithm, because it is going through an array and checking the *organization* of the data

---

### THE PROBLEM
```markdown
Given an integer array `nums`, return `true` if any value appears at least twice in the array, and return `false` if every element is distinct.
```
- go through an array (number[])
- return #boolean (true or false) if every element is unique
```javascript
/*
* @param {number[]} nums
* @return {boolean}
*/

var containsDuplicate = function(nums) {
	const seen = new Set();     // store our own values to sort

	for (let num of nums) {     // iterates through the list
		if (seen.has(num)) {    // check for duplicate
			return true;
		}
		seen.add(num);
	}

	return false;
};
```
---

### FLASHCARDS
the logic behind the "contains duplicate" problem is
?
creating a new variable (**new array**), iterate through the array (**for loop**), check for **duplicate**, return **boolean**

```javascript
var containsDuplicate = function(nums) {
	const seen = new Set();
	for (let num of nums) { 
		if (seen.has(num)) {    
			return true;
		}
		seen.add(num);          
	}

	return false;
};
```

