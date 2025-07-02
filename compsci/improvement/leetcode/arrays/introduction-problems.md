> the first set of array problems hosted on leetcode

all problems are written in [[java]]

### MAX CONSECUTIVE ONES
Given a binary array nums, return the maximum number of consecutive 1's in the array

### 1. *The Question Prompt*
```
Input: nums = [1,1,0,1,1,1]
Output: 3
Explanation: 3 1's in a row
```
### 2. *Coding the solution*
```java
class Solution {
  public int findMaxConsecutiveOnes(int[] nums) {
    int ans = 0;
    int sum = 0;

    for (final int num : nums)
      if (num == 1)
        ans = Math.max(ans, ++sum);
      else
        sum = 0;

    return ans;
  }
}

```

### FIND NUMBERS WITH EVEN NUMBER OF DIGITS
Given an array of nums of integers, return how many of them contain an even number of digits

### 1. *The Question Prompt*
```
Input: nums = [12, 345, 2, 6, 7869]
Output: 2 (12 = 2 digits and 7869 = 4 digits)
```
### 2. *Coding the Solution (in java)*
```java
class Solution {
	public int countDigit(int n) {
		return (int)Math.floor(Math.log10(n) + 1);
	}

	public int findNumbers(int[] nums) {
		int ans = 0, n = nums.length;
		for (int i = 0; i < n; i++) {
			if (countDigit(nums[i]) % 2 == 0)
				ans++;
		}
		return ans;
	}
}
```
### SQUARES OF A SORTED ARRAY
Given an integer array nums sorted in **non-decreasing** order, return *an array* of the squares of each number sorted in non-decreasing order

### 1. *The Question Prompt*
```
Input: nums = [-4, -1, 0, 3, 10]
Output: [0, 1, 9, 16, 100]
```

### 2. *Coding the solution (in java)*
```java
class Solution {
	public int[] sortedSquares(int[] A) {
		int[] res = new int[A.length];
		int lo = 0; int hi = A.length - 1;
		for (int i = A.length - 1; i >= 0; i--) {
			if (Math.abs(A[lo]) >= Math.abs(A[hi])) {
				res[i] = A[lo] * A[lo];
					lo++;
				} else {
					res[i] = A[hi] * A[hi];
					hi--;
				}
			}
		return res;
	}
}
```

