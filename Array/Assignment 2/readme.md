# Assignment no :- 2
### Question 1
Given an integer array nums of 2n integers, group these integers into n pairs
(a1, b1), (a2, b2),..., (an, bn) such that the sum of min(ai, bi) for all i is
maximized. Return the maximized sum.

Example 1:
Input: nums = [1,4,3,2]
Output: 4

Explanation: All possible pairings (ignoring the ordering of elements) are:

1. (1, 4), (2, 3) -> min(1, 4) + min(2, 3) = 1 + 2 = 3
2. (1, 3), (2, 4) -> min(1, 3) + min(2, 4) = 1 + 2 = 3
3. (1, 2), (3, 4) -> min(1, 2) + min(3, 4) = 1 + 3 = 4
So the maximum possible sum is 4
``` js 
function arrayPairSum(nums) {
  nums.sort((a, b) => a - b);

  let sum = 0;
  for (let i = 0; i < nums.length; i += 2) {
    sum += nums[i];
  }

  return sum;
}
```
#
### Question 2
Alice has n candies, where the ith candy is of type candyType[i]. Alice noticed
that she started to gain weight, so she visited a doctor.

The doctor advised Alice to only eat n / 2 of the candies she has (n is always
even). Alice likes her candies very much, and she wants to eat the maximum
number of different types of candies while still following the doctor's advice.

Given the integer array candyType of length n, return the maximum number of
different types of candies she can eat if she only eats n / 2 of them.

Example 1:
Input: candyType = [1,1,2,2,3,3]
Output: 3

Explanation: Alice can only eat 6 / 2 = 3 candies. Since there are only 3 types,
she can eat one of each type.
``` js 
function distributeCandies(candyType) {
  const maxEat = candyType.length / 2;
  const candySet = new Set(candyType);
  return Math.min(candySet.size, maxEat);
}
```
#
### Question 3
We define a harmonious array as an array where the difference between its
maximum value and its minimum value is exactly 1.

Given an integer array nums, return the length of its longest harmonious
subsequence among all its possible subsequences.

A subsequence of an array is a sequence that can be derived from the array by
deleting some or no elements without changing the order of the remaining
elements.

Example 1:
Input: nums = [1,3,2,2,5,2,3,7]
Output: 5

Explanation: The longest harmonious subsequence is [3,2,2,2,3].
``` js 
function findLHS(nums) {
  let maxLen = 0;
  const frequencyMap = new Map();
  for (const num of nums) {
    frequencyMap.set(num, (frequencyMap.get(num) || 0) + 1);
  }
  for (const num of nums) {
    if (frequencyMap.has(num + 1)) {
      const currentLen = frequencyMap.get(num) + frequencyMap.get(num + 1);
      maxLen = Math.max(maxLen, currentLen);
    }
  }

  return maxLen;
}
```
# 
### Question 4
You have a long flowerbed in which some of the plots are planted, and some are not.
However, flowers cannot be planted in adjacent plots.
Given an integer array flowerbed containing 0's and 1's, where 0 means empty and 1 means not empty, and an integer n, return true if n new flowers can be planted in the flowerbed without violating the no-adjacent-flowers rule and false otherwise.

Example 1:
Input: flowerbed = [1,0,0,0,1], n = 1
Output: true
``` js 
function canPlaceFlowers(flowerbed, n) {
  let count = 0;
  let i = 0;

  while (i < flowerbed.length) {
    if (
      flowerbed[i] === 0 &&
      (i === 0 || flowerbed[i - 1] === 0) &&
      (i === flowerbed.length - 1 || flowerbed[i + 1] === 0)
    ) {
      flowerbed[i] = 1;
      count++;
    }

    if (count >= n) {
      return true;
    }

    i++;
  }

  return false;
}
```
#
### Question 5
Given an integer array nums, find three numbers whose product is maximum and return the maximum product.

Example 1:
Input: nums = [1,2,3]
Output: 6
``` js 
function maximumProduct(nums) {
  nums.sort((a, b) => a - b); // Sort the array in ascending order

  const n = nums.length;
  const option1 = nums[0] * nums[1] * nums[n - 1];
  const option2 = nums[n - 1] * nums[n - 2] * nums[n - 3];
  return Math.max(option1, option2);
}
```
#
### Question 6
Given an array of integers nums which is sorted in ascending order, and an integer target,
write a function to search target in nums. If target exists, then return its index. Otherwise,
return -1.
You must write an algorithm with O(log n) runtime complexity.
Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
``` js 
function search(nums, target) {
  let left = 0;
  let right = nums.length - 1;

  while (left <= right) {
    const mid = Math.floor((left + right) / 2);

    if (nums[mid] === target) {
      return mid;
    } else if (nums[mid] < target) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }

  return -1;
}
```
#
### Question 7
An array is monotonic if it is either monotone increasing or monotone decreasing.
An array nums is monotone increasing if for all i <= j, nums[i] <= nums[j]. An array nums is monotone decreasing if for all i <= j, nums[i] >= nums[j].
Given an integer array nums, return true if the given array is monotonic, or false otherwise.

Example 1:
Input: nums = [1,2,2,3]
Output: true
``` js 
function checkMonotonic(array, size) {
  if (array.slice().sort((a, b) => b - a).every((value, index) => value === array[index])) {
    return true;
  }
  if (array.slice().sort((a, b) => a - b).every((value, index) => value === array[index])) {
    return true;
  }
  return false;
}

const array1 = [4, 5, 3, 2];
const array2 = [7, 0, 2, 1];
const array3 = [1, 2, 3];
const size1 = array1.length;
const size2 = array2.length;
const size3 = array3.length;

if (checkMonotonic(array1, size1)) {
  console.log("Is Monotonic ?: true");
} else {
  console.log("Is Monotonic ?: false");
}

if (checkMonotonic(array2, size2)) {
  console.log("Is Monotonic ?: true");
} else {
  console.log("Is Monotonic ?: false");
}

if (checkMonotonic(array3, size3)) {
  console.log("Is Monotonic ?: true");
} else {
  console.log("Is Monotonic ?: false");
}
```
#
### Question 8
You are given an integer array nums and an integer k.
In one operation, you can choose any index i where 0 <= i < nums.length and change nums[i] to nums[i] + x where x is an integer from the range [-k, k]. You can apply this operation at most once for each index i.
The score of nums is the difference between the maximum and minimum elements in nums.
Return the minimum score of nums after applying the mentioned operation at most once for each index in it.

Example 1:
Input: nums = [1], k = 0
Output: 0
``` js 
const arr = [1, 1, 2, 2, 3, 5, 4, 2, 2, 3, 1, 1, 1];
const n = arr.length;
const k = 4;

function printElements(arr, n, k) {
  const x = Math.floor(n / k);
  const mp = new Map();
  for (let i = 0; i < n; i++) {
    if (mp.has(arr[i])) {
      mp.set(arr[i], mp.get(arr[i]) + 1);
    } else {
      mp.set(arr[i], 1);
    }
  }
  for (let [key, value] of mp) {
    if (value > x) {
      console.log(key);
    }
  }
}

printElements(arr, n, k);
```

