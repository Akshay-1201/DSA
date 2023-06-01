# Assignment no :- 1
### Q1. Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.
You can return the answer in any order.

Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
``` js 
var twoSum = function(nums, target) {
    const hashmap = {};
    for (let i = 0; i < nums.length; i++) {
      const diff = target - nums[i];
      if (diff in hashmap) { // or, hashmap[diff] !== undefined
        return [hashmap[diff], i];
      }
  
      // Otherwise, add the current number to the hashmap.
      hashmap[nums[i]] = i;
    }
  
    return [];
  };

let nums = [1,2,4,3,5];
let target = 8;

console.log(twoSum(nums, target))
```
#
### Q2. Given an integer array nums and an integer val, remove all occurrences of val in nums in-place. The order of the elements may be changed. Then return the number of elements in nums which are not equal to val.

Consider the number of elements in nums which are not equal to val be k, to get accepted, you need to do the following things:

- Change the array nums such that the first k elements of nums contain the elements which are not equal to val. The remaining elements of nums are not important as well as the size of nums.
- Return k.

Example :
Input: nums = [3,2,2,3], val = 3
Output: 2, nums = [2,2,_*,_*]
``` js

var removeElement = function (nums, val) {
    let count = 0;
    for (let i = 0; i < nums.length; i++) {
        if (nums[i] !== val) {
            nums[count++] = nums[i];
        }
    }
    return count;
};
let arr = new Array(3,2,2,3);
let val = 3;
console.log(removeOccurence(arr,val));
console.log(...arr);
```
#
### Q3. Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with O(log n) runtime complexity.

Example 1:
Input: nums = [1,3,5,6], target = 5

Output: 2
``` js 
function findTheTarget(arr, target){
    let i=0; 
    let j = arr.length-1;

    while(i<=j){
        let mid = Math.floor((j+i)/2);

        if(arr[mid] == target){
            return mid;
        }else if(arr[mid] > target){
            j = mid-1;
        }else{
            i = mid+1;
        }
    }

    return i;
}


console.log(findTheTarget([1,3,4,6], ));
```
#
### Q4. You are given a large integer represented as an integer array digits, where each digits[i] is the ith digit of the integer. The digits are ordered from most significant to least significant in left-to-right order. The large integer does not contain any leading 0's.

Increment the large integer by one and return the resulting array of digits.

Example 1:
Input: digits = [1,2,3]
Output: [1,2,4]
``` js 
function addingOne(arr){
    let car = 1;
    for(let i=arr.length-1; i>=0; i--){
        let sum = arr[i]+car;
        arr[i] = sum%10;
        car = Math.floor(sum/10);
    }

    if(car> 0){
        arr.unshift(car);
    }
    return arr;
}


console.log(addingOne([9,8,9]));
```
#
### Q5. You are given two integer arrays nums1 and nums2, sorted in non-decreasing order, and two integers m and n, representing the number of elements in nums1 and nums2 respectively.

Merge nums1 and nums2 into a single array sorted in non-decreasing order.

The final sorted array should not be returned by the function, but instead be stored inside the array nums1. To accommodate this, nums1 has a length of m + n, where the first m elements denote the elements that should be merged, and the last n elements are set to 0 and should be ignored. nums2 has a length of n.

Example 1:
Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
Output: [1,2,2,3,5,6]

Explanation: The arrays we are merging are [1,2,3] and [2,5,6].
The result of the merge is [1,2,2,3,5,6] with the underlined elements coming from nums1.
``` js
var merge = function(nums1, m, nums2, n) {
    let i, j, k;

    for(i = m - 1, j = n - 1, k = m + n - 1; i >= 0 && j >= 0; k--){
        if(nums1[i] >= nums2[j]){
            nums1[k] = nums1[i--];
        } else {
            nums1[k] = nums2[j--];
        }
    }

    while(i >= 0) {
        nums1[k--] = nums1[i--];
    }

    while(j >= 0) {
        nums1[k--] = nums2[j--];
    }
};
```
#
### Q6. Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

Example 1:
Input: nums = [1,2,3,1]

Output: true
``` js
function isDistinct(arr){
    let ans = new Set(arr);
    return ans.size === arr.length;

    // return new Set(arr).size === arr.length;
}


console.log(isDistinct([1,2,8]));
console.log(isDistinct([1,2,6,1]));
```
# 
### Q7. Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the nonzero elements.

Note that you must do this in-place without making a copy of the array.

Example 1:
Input: nums = [0,1,0,3,12]
Output: [1,3,12,0,0]
``` js
function moveZeros(arr){
    let i=0;
    let j=0;

    while(j<arr.length){
        if(arr[j] != 0){
            arr[i] = arr[j];
            arr[j] = 0;

            i++;
        }
        j++;
    }

    return arr;
}


console.log(moveZeros([7,7,0,3,1,0,56,3,4,0,0]));
```
#
### Q8. You have a set of integers s, which originally contains all the numbers from 1 to n. Unfortunately, due to some error, one of the numbers in s got duplicated to another number in the set, which results in repetition of one number and loss of another number.

You are given an integer array nums representing the data status of this set after the error.

Find the number that occurs twice and the number that is missing and return them in the form of an array.

Example 1:
Input: nums = [1,2,2,4]
Output: [2,3]
``` js 
function findTheRepeatedValue(arr){
    let n = arr.length;
    let totalSum = Math.floor(n*(n+1)/2);

    let distinct = new Set(arr);

    let sum = 0;

    distinct.forEach((val)=>{
        sum += val;
    })

    return totalSum-sum;
}


console.log(findTheRepeatedValue([1,2,5,5]));
```
