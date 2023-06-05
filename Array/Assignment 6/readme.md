# Assignment No :- 6
###  Question 01
A permutation perm of n + 1 integers of all the integers in the range [0, n] can be represented as a string s of length n where:

s[i] == 'I' if perm[i] < perm[i + 1], and
s[i] == 'D' if perm[i] > perm[i + 1].
Given a string s, reconstruct the permutation perm and return it. If there are multiple valid permutations perm, return any of them.

Example:

Input: s = "IDID"
Output:[0,4,1,3,2]
``` js 
function reconstructPermutation(s) {
  const n = s.length;
  const permutation = [];
  let low = 0;
  let high = n;

  for (let i = 0; i < n; i++) {
    if (s[i] === "I") {
      permutation.push(low++);
    } else {
      permutation.push(high--);
    }
  }

  permutation.push(low);

  return permutation;
}
```
# 
###  Question 02
You are given an m x n integer matrix matrix with the following two properties:

Each row is sorted in non-decreasing order.
The first integer of each row is greater than the last integer of the previous row.
Given an integer target, return true if target is in matrix or false otherwise.

You must write a solution in O(log(m * n)) time complexity.

Example:


Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
Output: true
```js
function searchMatrix(matrix, target) {
  const m = matrix.length;
  const n = matrix[0].length;
  let low = 0;
  let high = m * n - 1;

  while (low <= high) {
    const mid = Math.floor((low + high) / 2);
    const row = Math.floor(mid / n);
    const col = mid % n;

    if (matrix[row][col] === target) {
      return true;
    } else if (matrix[row][col] < target) {
      low = mid + 1;
    } else {
      high = mid - 1;
    }
  }

  return false;
}
```
#
### Question 03
Given an array of integers arr, return true if and only if it is a valid mountain array.

Recall that arr is a mountain array if and only if:

arr.length >= 3
There exists some i with 0 < i < arr.length - 1 such that:
arr[0] < arr[1] < ... < arr[i - 1] < arr[i]
arr[i] > arr[i + 1] > ... > arr[arr.length - 1]

Example:

Input: arr = [2,1]
Output: false
```js
function validMountainArray(arr) {
  const n = arr.length;
  let i = 0;

  while (i + 1 < n && arr[i] < arr[i + 1]) {
    i++;
  }

  if (i === 0 || i === n - 1) {
    return false;
  }

  while (i + 1 < n && arr[i] > arr[i + 1]) {
    i++;
  }

  return i === n - 1;
}
```
#
### Question 04
Given a binary array nums, return the maximum length of a contiguous subarray with an equal number of 0 and 1.

Example:

Input: nums = [0,1]
Output: 2
Explanation:

[0, 1] is the longest contiguous subarray with an equal number of 0 and 1.
```js
function findMaxLength(nums) {
  const map = new Map();
  map.set(0, -1);
  let maxLength = 0;
  let count = 0;

  for (let i = 0; i < nums.length; i++) {
    count += nums[i] === 1 ? 1 : -1;

    if (map.has(count)) {
      maxLength = Math.max(maxLength, i - map.get(count));
    } else {
      map.set(count, i);
    }
  }

  return maxLength;
}
```
#
### Question 05
The product sum of two equal-length arrays a and b is equal to the sum of a[i] * b[i] for all 0 <= i < a.length (0-indexed).

For example, if a = [1,2,3,4] and b = [5,2,3,1], the product sum would be 1*5 + 2*2 + 3*3 + 4*1 = 22.
Given two arrays nums1 and nums2 of length n, return the minimum product sum if you are allowed to rearrange the order of the elements in nums1.

Example:

Input: nums1 = [5,3,4,2], nums2 = [4,2,2,5]
Output: 40
Explanation:

We can rearrange nums1 to become [3,5,4,2]. The product sum of [3,5,4,2] and [4,2,2,5] is 3*4 + 5*2 + 4*2 + 2*5 = 40.
```js
function minProductSum(nums1, nums2) {
  nums1.sort((a, b) => a - b);
  nums2.sort((a, b) => b - a);
  let minProductSum = 0;

  for (let i = 0; i < nums1.length; i++) {
    minProductSum += nums1[i] * nums2[i];
  }

  return minProductSum;
}
```
#
### Question 06
An integer array original is transformed into a doubled array changed by appending twice the value of every element in original, and then randomly shuffling the resulting array.

Given an array changed, return original if changed is a doubled array. If changed is not a doubled array, return an empty array. The elements in original may be returned in any order.

Example:

Input: changed = [1,3,4,2,6,8]
Output: [1,3,4]
Explanation: One possible original array could be [1,3,4]:

Twice the value of 1 is 1 * 2 = 2.
Twice the value of 3 is 3 * 2 = 6.
Twice the value of 4 is 4 * 2 = 8.
Other original arrays could be [4,3,1] or [3,1,4].
``` js 
function findOriginalArray(changed) {
  if (changed.length % 2 !== 0) {
    return [];
  }

  const counts = new Map();

  for (const num of changed) {
    counts.set(num, (counts.get(num) || 0) + 1);
  }

  const original = [];

  changed.sort((a, b) => a - b);

  for (const num of changed) {
    if (counts.get(num) === 0) {
      continue;
    }

    const doubledNum = num * 2;

    if (counts.get(doubledNum) === 0) {
      return [];
    }

    original.push(num);
    counts.set(num, counts.get(num) - 1);
    counts.set(doubledNum, counts.get(doubledNum) - 1);
  }

  return original;
}
```
#
### Given a positive integer n, generate an n x n matrix filled with elements from 1 to n2 in spiral order.

Example:


Input: n = 3
Output: [[1,2,3],[8,9,4],[7,6,5]]
```js
function generateMatrix(n) {
  const matrix = Array.from({ length: n }, () => Array(n).fill(0));
  let left = 0,
    right = n - 1,
    top = 0,
    bottom = n - 1;
  let num = 1;

  while (num <= n * n) {
    for (let i = left; i <= right; i++) {
      matrix[top][i] = num++;
    }
    top++;

    for (let i = top; i <= bottom; i++) {
      matrix[i][right] = num++;
    }
    right--;

    for (let i = right; i >= left; i--) {
      matrix[bottom][i] = num++;
    }
    bottom--;

    for (let i = bottom; i >= top; i--) {
      matrix[i][left] = num++;
    }
    left++;
  }

  return matrix;
}
```
#
### Question 08
Given two sparse matrices mat1 of size m x k and mat2 of size k x n, return the result of mat1 x mat2. You may assume that multiplication is always possible.

Example:


Input: mat1 = [[1,0,0],[-1,0,3]], mat2 = [[7,0,0],[0,0,0],[0,0,1]]
Output: [[7,0,0],[-7,0,3]]
```js
function multiply(mat1, mat2) {
  const m = mat1.length;
  const k = mat1[0].length;
  const n = mat2[0].length;
  const result = Array.from({ length: m }, () => Array(n).fill(0));

  for (let i = 0; i < m; i++) {
    for (let j = 0; j < n; j++) {
      for (let l = 0; l < k; l++) {
        result[i][j] += mat1[i][l] * mat2[l][j];
      }
    }
  }

  return result;
}
```
