# Assignment no 7
### Question 01
Given two strings s and t, determine if they are isomorphic.

Two strings s and t are isomorphic if the characters in s can be replaced to get t.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character, but a character may map to itself.

Example:

Input: s = "egg", t = "add"
Output: true
``` js 
function isIsomorphic(s, t) {
  if (s.length !== t.length) {
    return false;
  }

  const sMap = new Map();
  const tMap = new Map();

  for (let i = 0; i < s.length; i++) {
    const charS = s[i];
    const charT = t[i];

    if (
      (sMap.has(charS) && sMap.get(charS) !== charT) ||
      (tMap.has(charT) && tMap.get(charT) !== charS)
    ) {
      return false;
    }

    sMap.set(charS, charT);
    tMap.set(charT, charS);
  }

  return true;
}
```
#
### Question 02
Given a string num which represents an integer, return true if num is a strobogrammatic number.

A strobogrammatic number is a number that looks the same when rotated 180 degrees (looked at upside down).

Example:

Input: num = "69"
Output: true
```js
function isStrobogrammatic(num) {
  const map = new Map([
    ["0", "0"],
    ["1", "1"],
    ["6", "9"],
    ["8", "8"],
    ["9", "6"],
  ]);

  let left = 0;
  let right = num.length - 1;

  while (left <= right) {
    if (!map.has(num[left]) || map.get(num[left]) !== num[right]) {
      return false;
    }

    left++;
    right--;
  }

  return true;
}
```
# 
### Question 03
Given two non-negative integers, num1 and num2 represented as string, return the sum of num1 and num2 as a string.

You must solve the problem without using any built-in library for handling large integers (such as BigInteger). You must also not convert the inputs to integers directly.

Example:

Input: num1 = "11", num2 = "123"
Output: "134"
```js
function addStrings(num1, num2) {
  let i = num1.length - 1;
  let j = num2.length - 1;
  let carry = 0;
  let result = "";

  while (i >= 0 || j >= 0 || carry > 0) {
    let sum = carry;

    if (i >= 0) {
      sum += parseInt(num1[i]);
      i--;
    }

    if (j >= 0) {
      sum += parseInt(num2[j]);
      j--;
    }

    carry = Math.floor(sum / 10);
    sum = sum % 10;
    result = sum + result;
  }

  return result;
}
```
#
###  Question 04
Given a string s, reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.

Example:

Input: s = "Let's take LeetCode contest"
Output: "s'teL ekat edoCteeL tsetnoc"
```js
function reverseWords(s) {
  const words = s.split(" ");

  for (let i = 0; i < words.length; i++) {
    words[i] = words[i].split("").reverse().join("");
  }

  return words.join(" ");
}
```
#
### Question 05
Given a string s and an integer k, reverse the first k characters for every 2k characters counting from the start of the string.

If there are fewer than k characters left, reverse all of them. If there are less than 2k but greater than or equal to k characters, then reverse the first k characters and leave the other as original.

Example:

Input: s = "abcdefg", k = 2
Output: "bacdfeg"
```js
function reverseStr(s, k) {
  const arr = s.split("");

  for (let i = 0; i < arr.length; i += 2 * k) {
    let start = i;
    let end = Math.min(i + k - 1, arr.length - 1);

    while (start < end) {
      const temp = arr[start];
      arr[start] = arr[end];
      arr[end] = temp;
      start++;
      end--;
    }
  }

  return arr.join("");
}
```
#
### Question 06
Given two strings s and goal, return true if and only if s can become goal after some number of shifts on s.

A shift on s consists of moving the leftmost character of s to the rightmost position.

For example, if s = "abcde", then it will be "bcdea" after one shift.
Example:

Input: s = "abcde", goal = "cdeab"
Output: true
```js
function rotateString(s, goal) {
  if (s.length !== goal.length) {
    return false;
  }

  if (s === goal) {
    return true;
  }

  for (let i = 0; i < s.length; i++) {
    const rotatedString = s.slice(i) + s.slice(0, i);
    if (rotatedString === goal) {
      return true;
    }
  }

  return false;
}
```
#
### Question 07
Given two strings s and t, return true if they are equal when both are typed into empty text editors. '#' means a backspace character.

Note that after backspacing an empty text, the text will continue empty.

Example:

Input: s = "ab#c", t = "ad#c"
Output: true
Explanation:

Both s and t become "ac".
```js
function backspaceCompare(s, t) {
  return buildString(s) === buildString(t);
}

function buildString(str) {
  const result = [];

  for (let char of str) {
    if (char !== "#") {
      result.push(char);
    } else {
      result.pop();
    }
  }

  return result.join("");
}
```
#
###  Question 08
You are given an array coordinates, coordinates[i] = [x, y], where [x, y] represents the coordinate of a point. Check if these points make a straight line in the XY plane.

Example:


Input: coordinates = [[1,2],[2,3],[3,4],[4,5],[5,6],[6,7]]
Output: true
```js
function checkStraightLine(coordinates) {
  const [x0, y0] = coordinates[0];
  const [x1, y1] = coordinates[1];
  const slope = (y1 - y0) / (x1 - x0);

  for (let i = 2; i < coordinates.length; i++) {
    const [x, y] = coordinates[i];
    const currentSlope = (y - y0) / (x - x0);

    if (currentSlope !== slope) {
      return false;
    }
  }

  return true;
}
``` 