# DSA-PREPERATIONS
Detailed analysis on mostly asked interview questions.

# 1. Two Sum

---

## Problem Statement

Given an array of integers `nums` and an integer `target`, **return the indices** of the two numbers in the array such that they add up to the target. Assume exactly one solution exists, and you cannot use the same element twice.

---

## Sample Input
nums = [2, 7, 11, 15], target = 9


---

## Sample Output
[0, 1]

---


## Detailed Explanation:

nums[0] + nums[1] = 2 + 7 = 9, which equals the target.


The naive approach is to check every pair to see if they sum to the target, which involves nested loops and results in O(n²) time complexity.

An optimal solution uses a hash map (object in JavaScript):

Iterate through the array once.
For each number, calculate the complement needed to reach the target (complement = target - nums[i]).
Check if this complement exists in the map.
If yes, return the indices immediately.
If no, add the current number and its index to the map.



## solution 1 (Using Hashmap)
Time: O(n) — single pass.

Space: O(n) — store all numbers in map.

```js 

function twoSum(nums, target) {
  const map = new Map();

  for (let i = 0; i < nums.length; i++) {
    const complement = target - nums[i];
    if (map.has(complement)) {
      return [map.get(complement), i];
    }
    map.set(nums[i], i);
  }
  return [];
}


```
## solution 2 (Using two pointers)
Time: O(n log n) due to sorting.

Space: O(n) for the mapped array, but you can mutate original array if allowed to avoid extra space.

```js 

function twoSum(nums, target) {
  const numsWithIndex = nums.map((num, idx) => ({ num, idx }));
  numsWithIndex.sort((a, b) => a.num - b.num);

  let left = 0;
  let right = numsWithIndex.length - 1;

  while (left < right) {
    const sum = numsWithIndex[left].num + numsWithIndex[right].num;
    if (sum === target) {
      return [numsWithIndex[left].idx, numsWithIndex[right].idx];
    } else if (sum < target) {
      left++;
    } else {
      right--;
    }
  }

  return [];
}


```

