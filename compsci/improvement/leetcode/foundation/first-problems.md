> The beginning of the leetcode journey.

*How to break into leetcode?*
- find the "beginner challenge course"
	- go through each module and learn the **logic** and **reasoning** of the problems
	- Introduction problems are in [[java]]

### PROBLEM 1 - 1480. Running Sum of 1D Array 
This problem introduces the **prefix sum array** and how to build one:
### 1. *The Question Prompt*
```
Input: nums = [3, 1, 2, 10, 1]
Output: [3, 4, 6, 16, 17]
```
---
### 2. *Breaking down the math of the question in CODE* 
```java
runningSum[i] = sum{nums[0]... nums[i]} 
```
Translation: How to calculate a running sum

Here is a **visual representation**:
![[runningsum.excalidraw]]

---
### 3. *Coding the solution (in java)* 
```java
class Solution {
	public int[] runningSum(int[] nums) {
		int[] results = new int[nums.length];
		results[0] = nums[0]; 

		for (int i = 1; 1 < nums.length; i++) {
			results[i] = nums[i] + results[i - 1];
		}
                              
		return results = 0(n)
	}

	// time complexity = 0(n)
	// space complexity = 0(1)
}
```
---



### PROBLEM 2 - 1672. Richest Customer Wealth (2D Arrays)
This problem introduces **data** stored in arrays with *2 (or more) dimensions*
### 1. *The Question Prompt*
```
Input: accounts = [ [7,1,3], [2,8,7], [1,9,5] ]
Output: 17
```
```
CONTRAINTS
- m == accounts.length
- n == accounts[i].length
- 1 <= m, n <= 50
- 1 <= accounts[i][j] <= 100
```

---

### 2. *Coding the solution (in java)* 
```java
class Solution {
	public int maximumWealth(int[][] accounts) {
		int maxWealthSoFar = 0; // initialize a variable for starting value

		for (int[] customer : accounts) { //creates variable for sum of "row"
			int currentCustomerWealth - 0;

			for (int bank : customer) { // 
				currentCustomerWealth +- bank; // adds each bank (layered loop)	
			}
	
			maxWealthSoFar = Math.max(maxWealthSoFar, currentCusomterWealth);
			
			// Overwrites the maxWealthSoFar if currentCustomer is greater
			// > done by picking the bigger value (with Math.max)
			// > writes the same maxWealthSoFar if currentCustomer is less
		}

		return maxWealthSoFar;
	} 

	// Time complexity =  0(n)
	// Space Complexity = 0(1) 
}
```
---

### 3. *Demonstrating how computers VISUALIZE data* 

![[data-arrays.excalidraw]]

---

### PROBLEM 3 - 412. Fizz Buzz (logic to code conversion)
This problem introduces how to **convert** logic into **code**
### 1. *The Question Prompt*

```
CONSTRAINTS:
answer[i] == "FizzBuzz" if i is divisible by 3 and 5
answer[i] == "Fizz" if i is divisible by 3
answer[i] == "Buzz" if i is divisble by 5
answer[i] == i (as a string) if none of the above

Input: n = 5 (assigning index number of 5)
Output: ["1", "2", "Fizz", "4", "Buzz"]
```

---
### 2.  *Coding the solution (in java)
```java
class Solution {
	public List<String> fizzBuzz(int n) {
		List<String> answer = new Arraylist<>(n); // initialize with n items

		// answer is just NAMING the variable with a value of List<String>

		for (int i = 1; i <= n; i++) {
			boolean divisbileBy3 = i % 3 == 0; // divisible by 3 with no rmdr
			boolean divisbileBy3 = i % 5 == 0; // divisbile by 5 with no rmdr

			// Needed to create an ADDITIONAL condition (booleans)
			// Associate string and int without a condition (applies to loop)

			if (divisbleBy3 && divsibleBy5) {
				answer.add("FizzBuzz");
			} else if (divisbleBy3) {
				answer.add("Fizz");
			} else if (divisibleBy5) {
				answer.add("Buzz");
			} else {
				answer.add(String.valueOf(i));
			}
		}

		return answer;
	}

	// Time complexity = O(n)
	// Space complexity = O(1) -- one varibale... answer
}
```
--- 


### PROBLEM 4 - 1342. Number of Steps to Reduce a Number to Zero
Learn how to identify if a number is even or odd then find **steps to zero**
### 1. *The Question Prompt*
```
"Return the numbers of steps to zero"

Rules for each "step"
1. Divde even integers by 2
2. Subtract 1 from odd integers
- Repeat until 0

CONSTRAINTS:
0 <= num <= 10^6

Input: n = 14
Output = 6 (14 - 7 6 3 2 1 0)
```
---
### 2.  *Coding the solution (in java)
```java

// Time complexity: O(logn)
// Halving Step + Subtracting Step = 2logn = O(logn)

class Solution {
	public int numberOfSteps(int num) {
		int steps = 0;

		while (num > 0) {
			if (num % 2 == 0) { // divisble by 2
				num /= 2; // num = num / 2... divides and assigns back to num
			} else {
				num--; // subtracts 1 and assigns back to num
			}
			steps++;
		}
		return steps;
	}

	// Time Complexity = O(logn)
	// Space Complexity = O(1)

	// binary --> list of booleans (1's and 0's)
	// depends on condition arguments
}


```
---

### 3. *Advanced concepts mentioned in the problem*
- Binary Representation of integers
- Bitwise Shift Operators
- Bitwise Logical Operators
- Bitmasks

---





### PROBLEM 5 - 876. Middle of The Linked List
This problem introduces a new data structure, the **linked list**
### 1. *The Question Prompt*
```
Given the HEAD of a singly linked list, return the middle node of the linked list.

CONSTRAINTS:
- 1 <= total number of nodes <= 100
- 1 <= Node.val <= 100

Input: [1,2,3,4,5]
Output: [3,4,5]

```
---
### 2. *Coding the solution (in java)*
```java

// Time Complexity = O(n)
// Space Complexity = O(1)

class Solution {
	public ListNode middleNode(listNode head) {
		ListNode middle = head;
		ListNode end = head;

		while (end != null && end.next != null) {
			middle = middle.next;
			end = end.next.next;

			reutrn middle;
		} 
	}
}

```
---
### 3. *Visualizing the Linked List*
![[linked-list.excalidraw]]

---



### PROBLEM 6 - 383. Ransom Note
This problem introduces the **hash map** (or dictionary) data structure
### 1. *The Question Prompt*
```
Input: ransomNote= "aa", maagzine= "ab"
Output: false

Input ransomNote= "aa", magazine= "aab"
Output: True

Can the letters in the magazine string construct the string in ransomNote?

```
---
### 2. *Coding the solution (in java)*
```java

// Time Complexity = O(m)
// Space Complexity = O(1)

class Solution {
	public boolean conConstruct(String ransomNote, String magazine) {
		HashMap<Character, Integer> magazineLetters = new HashmMap<>();

		for (int i = 0; i < magazine.length(); i++) {
			char m = maagazine.charAt(i);

			int currentCount = magazineLetters.getOrDefault(m, 0);
			magazineLetters.put(m, currentCount + 1);
		}

		for (int = 0; i < ransomNote.length(); i++;) {
			char r = ransomNote.charAt(i);

			int currentCount = magazineLetters.getOrDefault(r, 0);

			if (currentCount == 0) {
				return false;
			}

			magazineLetters.put(r, currentCount - 1);
		}

		return true;
	}
}

```
---
### 3. Visualizing a Hash map

![[hashmap.excalidraw]]

---

