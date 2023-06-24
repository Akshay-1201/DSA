# Assignment No :- 17
### Question 01
Given a string s, find the first non-repeating character in it and return its index. If it does not exist, return -1.

Example 1:

Input: s = "leetcode"
Output: 0
Example 2:

Input: s = "loveleetcode"
Output: 2
Example 3:

Input: s = "aabb"
Output: -1
```js
function firstNonRepeatingCharacter(s) {
  const charCount = new Map();

  for (let i = 0; i < s.length; i++) {
    const char = s[i];
    charCount.set(char, (charCount.get(char) || 0) + 1);
  }

  for (let i = 0; i < s.length; i++) {
    const char = s[i];
    if (charCount.get(char) === 1) {
      return i;
    }
  }

  return -1;
}
```
#
### Question 02
Given a circular integer array nums of length n, return the maximum possible sum of a non-empty subarray of nums.

A circular array means the end of the array connects to the beginning of the array. Formally, the next element of nums[i] is nums[(i + 1) % n] and the previous element of nums[i] is nums[(i - 1 + n) % n].

A subarray may only include each element of the fixed buffer nums at most once. Formally, for a subarray nums[i], nums[i + 1], ..., nums[j], there does not exist i <= k1, k2 <= j with k1 % n == k2 % n.

Example 1:

Input: nums = [1,-2,3,-2]
Output: 3
Explanation: Subarray [3] has maximum sum 3.

Example 2:

Input: nums = [5,-3,5]
Output: 10
Explanation: Subarray [5,5] has maximum sum 5 + 5 = 10.

Example 3:

Input: nums = [-3,-2,-3]
Output: -2
Explanation: Subarray [-2] has maximum sum -2.
```js
function maxSubarraySumCircular(nums) {
  const n = nums.length;

  let maxSum = -Infinity;
  let currentMax = 0;

  for (let i = 0; i < n; i++) {
    currentMax = Math.max(nums[i], currentMax + nums[i]);
    maxSum = Math.max(maxSum, currentMax);
  }

  let minSum = Infinity;
  let currentMin = 0;
  let totalSum = 0;

  for (let i = 0; i < n; i++) {
    currentMin = Math.min(nums[i], currentMin + nums[i]);
    minSum = Math.min(minSum, currentMin);
    totalSum += nums[i];
  }

  if (maxSum > 0) {
    return Math.max(maxSum, totalSum - minSum);
  } else {
    return maxSum;
  }
}
```
#
### Question 03
The school cafeteria offers circular and square sandwiches at lunch break, referred to by numbers 0 and 1 respectively. All students stand in a queue. Each student either prefers square or circular sandwiches.

The number of sandwiches in the cafeteria is equal to the number of students. The sandwiches are placed in a stack. At each step:

If the student at the front of the queue prefers the sandwich on the top of the stack, they will take it and leave the queue.
Otherwise, they will leave it and go to the queue's end.
This continues until none of the queue students want to take the top sandwich and are thus unable to eat.

You are given two integer arrays students and sandwiches where sandwiches[i] is the type of the ith sandwich in the stack (i = 0 is the top of the stack) and students[j] is the preference of the jth student in the initial queue (j = 0 is the front of the queue). Return the number of students that are unable to eat.

Example 1:

Input: students = [1,1,0,0], sandwiches = [0,1,0,1]
Output: 0
Explanation:
- Front student leaves the top sandwich and returns to the end of the line making students = [1,0,0,1].
- Front student leaves the top sandwich and returns to the end of the line making students = [0,0,1,1].
- Front student takes the top sandwich and leaves the line making students = [0,1,1] and sandwiches = [1,0,1].
- Front student leaves the top sandwich and returns to the end of the line making students = [1,1,0].
- Front student takes the top sandwich and leaves the line making students = [1,0] and sandwiches = [0,1].
- Front student leaves the top sandwich and returns to the end of the line making students = [0,1].
- Front student takes the top sandwich and leaves the line making students = [1] and sandwiches = [1].
- Front student takes the top sandwich and leaves the line making students = [] and sandwiches = [].
Hence all students are able to eat.
Example 2:

Input: students = [1,1,1,0,0,1], sandwiches = [1,0,0,0,1,1]
Output: 3
```js
function countStudents(students, sandwiches) {
  const count = [0, 0];

  for (let pref of students) {
    count[pref]++;
  }

  for (let i = 0; i < sandwiches.length; i++) {
    if (count[sandwiches[i]] > 0) {
      count[sandwiches[i]]--;
    } else {
      return students.length - i;
    }
  }

  return 0;
}
```
#
### Question 04
You have a RecentCounter class which counts the number of recent requests within a certain time frame.

Implement the RecentCounter class:

RecentCounter() Initializes the counter with zero recent requests.
int ping(int t) Adds a new request at time t, where t represents some time in milliseconds, and returns the number of requests that has happened in the past 3000 milliseconds (including the new request). Specifically, return the number of requests that have happened in the inclusive range [t - 3000, t].
It is guaranteed that every call to ping uses a strictly larger value of t than the previous call.

Example 1:

Input
["RecentCounter", "ping", "ping", "ping", "ping"]
[[], [1], [100], [3001], [3002]]
Output
[null, 1, 2, 3, 3]

Explanation
RecentCounter recentCounter = new RecentCounter();
recentCounter.ping(1);     // requests = [1], range is [-2999,1], return 1
recentCounter.ping(100);   // requests = [1,100], range is [-2900,100], return 2
recentCounter.ping(3001);  // requests = [1,100,3001], range is [1,3001], return 3
recentCounter.ping(3002);  // requests = [1,100,3001,3002], range is [2,3002], return 3
```js
class RecentCounter {
  constructor() {
    this.requests = [];
  }

  ping(t) {
    this.requests.push(t);

    while (this.requests[0] < t - 3000) {
      this.requests.shift();
    }

    return this.requests.length;
  }
}
```
#
### Question 05
There are n friends that are playing a game. The friends are sitting in a circle and are numbered from 1 to n in clockwise order. More formally, moving clockwise from the ith friend brings you to the (i+1)th friend for 1 <= i < n, and moving clockwise from the nth friend brings you to the 1st friend.

The rules of the game are as follows:

Start at the 1st friend.
Count the next k friends in the clockwise direction including the friend you started at. The counting wraps around the circle and may count some friends more than once.
The last friend you counted leaves the circle and loses the game.
If there is still more than one friend in the circle, go back to step 2 starting from the friend immediately clockwise of the friend who just lost and repeat.
Else, the last friend in the circle wins the game.
Given the number of friends, n, and an integer k, return the winner of the game.

Example 1:


Input: n = 5, k = 2
Output: 3
Explanation: Here are the steps of the game:
1) Start at friend 1.
2) Count 2 friends clockwise, which are friends 1 and 2.
3) Friend 2 leaves the circle. Next start is friend 3.
4) Count 2 friends clockwise, which are friends 3 and 4.
5) Friend 4 leaves the circle. Next start is friend 5.
6) Count 2 friends clockwise, which are friends 5 and 1.
7) Friend 1 leaves the circle. Next start is friend 3.
8) Count 2 friends clockwise, which are friends 3 and 5.
9) Friend 5 leaves the circle. Only friend 3 is left, so they are the winner.
Example 2:

Input: n = 6, k = 5
Output: 1
Explanation: The friends leave in this order: 5, 4, 6, 2, 3. The winner is friend 1.
```js
function findTheWinner(n, k) {
  let winner = 0;

  for (let i = 2; i <= n; i++) {
    winner = (winner + k) % i;
  }

  return winner + 1;
}
```
#
### Question 06
You are given an integer array deck. There is a deck of cards where every card has a unique integer. The integer on the ith card is deck[i].

You can order the deck in any order you want. Initially, all the cards start face down (unrevealed) in one deck.

You will do the following steps repeatedly until all cards are revealed:

Take the top card of the deck, reveal it, and take it out of the deck.
If there are still cards in the deck then put the next top card of the deck at the bottom of the deck.
If there are still unrevealed cards, go back to step 1. Otherwise, stop.
Return an ordering of the deck that would reveal the cards in increasing order.

Note that the first entry in the answer is considered to be the top of the deck.

Example 1:

Input: deck = [17,13,11,2,3,5,7]
Output: [2,13,3,11,5,17,7]
Explanation:
We get the deck in the order [17,13,11,2,3,5,7] (this order does not matter), and reorder it.
After reordering, the deck starts as [2,13,3,11,5,17,7], where 2 is the top of the deck.
We reveal 2, and move 13 to the bottom.  The deck is now [3,11,5,17,7,13].
We reveal 3, and move 11 to the bottom.  The deck is now [5,17,7,13,11].
We reveal 5, and move 17 to the bottom.  The deck is now [7,13,11,17].
We reveal 7, and move 13 to the bottom.  The deck is now [11,17,13].
We reveal 11, and move 17 to the bottom.  The deck is now [13,17].
We reveal 13, and move 17 to the bottom.  The deck is now [17].
We reveal 17.
Since all the cards revealed are in increasing order, the answer is correct.
Example 2:

Input: deck = [1,1000]
Output: [1,1000]
```js
function deckRevealedIncreasing(deck) {
  deck.sort((a, b) => a - b);

  const result = [];
  const queue = [...deck];

  while (queue.length) {
    result.push(queue.shift());
    if (queue.length) {
      queue.push(queue.shift());
    }
  }

  return result;
}
```
#
### Question 07
Design a queue that supports push and pop operations in the front, middle, and back.

Implement the FrontMiddleBack class:

FrontMiddleBack() Initializes the queue.
void pushFront(int val) Adds val to the front of the queue.
void pushMiddle(int val) Adds val to the middle of the queue.
void pushBack(int val) Adds val to the back of the queue.
int popFront() Removes the front element of the queue and returns it. If the queue is empty, return 1.
int popMiddle() Removes the middle element of the queue and returns it. If the queue is empty, return 1.
int popBack() Removes the back element of the queue and returns it. If the queue is empty, return 1.
Notice that when there are two middle position choices, the operation is performed on the frontmost middle position choice. For example:

Pushing 6 into the middle of [1, 2, 3, 4, 5] results in [1, 2, 6, 3, 4, 5].
Popping the middle from [1, 2, 3, 4, 5, 6] returns 3 and results in [1, 2, 4, 5, 6].
Example 1:

Input:
["FrontMiddleBackQueue", "pushFront", "pushBack", "pushMiddle", "pushMiddle", "popFront", "popMiddle", "popMiddle", "popBack", "popFront"]
[[], [1], [2], [3], [4], [], [], [], [], []]
Output:
[null, null, null, null, null, 1, 3, 4, 2, -1]

Explanation:
FrontMiddleBackQueue q = new FrontMiddleBackQueue();
q.pushFront(1);   // [1]
q.pushBack(2);    // [1,2]
q.pushMiddle(3);  // [1,3, 2]
q.pushMiddle(4);  // [1,4, 3, 2]
q.popFront();     // return 1 -> [4, 3, 2]
q.popMiddle();    // return 3 -> [4, 2]
q.popMiddle();    // return 4 -> [2]
q.popBack();      // return 2 -> []
q.popFront();     // return -1 -> [] (The queue is empty)
```js
class FrontMiddleBackQueue {
  constructor() {
    this.queue = [];
  }

  pushFront(val) {
    this.queue.unshift(val);
  }

  pushMiddle(val) {
    const mid = Math.floor(this.queue.length / 2);
    this.queue.splice(mid, 0, val);
  }

  pushBack(val) {
    this.queue.push(val);
  }

  popFront() {
    if (this.queue.length === 0) {
      return -1;
    }
    return this.queue.shift();
  }

  popMiddle() {
    if (this.queue.length === 0) {
      return -1;
    }
    const mid = Math.floor((this.queue.length - 1) / 2);
    return this.queue.splice(mid, 1)[0];
  }

  popBack() {
    if (this.queue.length === 0) {
      return -1;
    }
    return this.queue.pop();
  }
}
```
#
### Question 08
For a stream of integers, implement a data structure that checks if the last k integers parsed in the stream are equal to value.

Implement the DataStream class:

DataStream(int value, int k) Initializes the object with an empty integer stream and the two integers value and k.
boolean consec(int num) Adds num to the stream of integers. Returns true if the last k integers are equal to value, and false otherwise. If there are less than k integers, the condition does not hold true, so returns false.
Example 1:

Input
["DataStream", "consec", "consec", "consec", "consec"]
[[4, 3], [4], [4], [4], [3]]
Output
[null, false, false, true, false]

Explanation
DataStream dataStream = new DataStream(4, 3); //value = 4, k = 3
dataStream.consec(4); // Only 1 integer is parsed, so returns False.
dataStream.consec(4); // Only 2 integers are parsed.
                      // Since 2 is less than k, returns False.
dataStream.consec(4); // The 3 integers parsed are all equal to value, so returns True.
dataStream.consec(3); // The last k integers parsed in the stream are [4,4,3].
                      // Since 3 is not equal to value, it returns False.
```js
class DataStream {
  constructor(value, k) {
    this.stream = [];
    this.value = value;
    this.k = k;
  }

  consec(num) {
    this.stream.push(num);
    if (this.stream.length < this.k) {
      return false;
    }

    for (let i = this.stream.length - this.k; i < this.stream.length; i++) {
      if (this.stream[i] !== this.value) {
        return false;
      }
    }

    return true;
  }
}
```