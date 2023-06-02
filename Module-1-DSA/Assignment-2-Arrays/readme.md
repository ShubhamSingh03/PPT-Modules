# Assignment-2 Questions & Solutions

💡 **Question-1:** Given an integer array nums of 2n integers, group these integers into n pairs (a1, b1), (a2, b2),..., (an, bn) such that the sum of min(ai, bi) for all i is maximized. Return the maximized sum.
Example:
Input: nums = [1,4,3,2]
Output: 4

💬 **Solution-1:**

```js
function arrayPairSum(nums) {
  nums.sort((a, b) => a - b);
  let maxSum = 0;
  for (let i = 0; i < nums.length; i += 2) {
    maxSum += nums[i];
  }
  return maxSum;
}

//Example:
const nums = [1, 4, 3, 2];
const result = arrayPairSum(nums);
console.log(result); // Output: 4


```

<hr/>

💡 **Question-2:** Alice has n candies, where the ith candy is of type candyType[i]. Alice noticed that she started to gain weight, so she visited a doctor. 

The doctor advised Alice to only eat n / 2 of the candies she has (n is always even). Alice likes her candies very much, and she wants to eat the maximum number of different types of candies while still following the doctor's advice. 

Given the integer array candyType of length n, return the maximum number of different types of candies she can eat if she only eats n / 2 of them.
Example:
Input: candyType = [1,1,2,2,3,3]
Output: 3

💬 **Solution-2:**

```js
function maxCandies(candyType) {
  const uniqueCandies = new Set();
  for (let i = 0; i < candyType.length; i++) {
    uniqueCandies.add(candyType[i]);
  }
  const maxCandies = Math.min(uniqueCandies.size, candyType.length / 2);
  return maxCandies;
}

// Example:
const candyType = [1, 1, 2, 2, 3, 3];
const result = maxCandies(candyType);
console.log(result); // Output: 3

```

<hr/>

💡 **Question-3:** We define a harmonious array as an array where the difference between its maximum value
and its minimum value is exactly 1.

Given an integer array nums, return the length of its longest harmonious subsequence
among all its possible subsequences.

A subsequence of an array is a sequence that can be derived from the array by deleting some or no elements without changing the order of the remaining elements.

Example:
Input: nums = [1,3,2,2,5,2,3,7]
Output: 5

💬 **Solution-3:**

```js
function findLHS(nums) {
  const numFreq = new Map();
  for (let num of nums) {
    numFreq.set(num, (numFreq.get(num) || 0) + 1);
  }

  let maxLen = 0;
  for (let [num, freq] of numFreq) {
    if (numFreq.has(num + 1)) {
      maxLen = Math.max(maxLen, freq + numFreq.get(num + 1));
    }
  }

  return maxLen;
}

// Example:
const nums = [1, 3, 2, 2, 5, 2, 3, 7];
const result = findLHS(nums);
console.log(result); // Output: 5

```

<hr/>

💡 **Question-4:** You have a long flowerbed in which some of the plots are planted, and some are not.
However, flowers cannot be planted in adjacent plots.
Given an integer array flowerbed containing 0's and 1's, where 0 means empty and 1 means not empty, and an integer n, return true if n new flowers can be planted in the flowerbed without violating the no-adjacent-flowers rule and false otherwise.

Example:
Input: flowerbed = [1,0,0,0,1], n = 1
Output: true

💬 **Solution-4:**

```js
function canPlaceFlowers(flowerbed, n) {
  let count = 0;
  for (let i = 0; i < flowerbed.length; i++) {
    if (
      flowerbed[i] === 0 &&
      (i === 0 || flowerbed[i - 1] === 0) &&
      (i === flowerbed.length - 1 || flowerbed[i + 1] === 0)
    ) {
      count++;
      flowerbed[i] = 1;
    }
  }
  return count >= n;
}

// Example:
const flowerbed = [1, 0, 0, 0, 1];
const n = 1;
const result = canPlaceFlowers(flowerbed, n);
console.log(result); // Output: true

```

<hr/>

💡 **Question-5:** Given an integer array nums, find three numbers whose product is maximum and return the maximum product.

Example:
Input: nums = [1,2,3]
Output: 6

💬 **Solution-5:**

```js
function maximumProduct(nums) {
  nums.sort((a, b) => a - b);
  const n = nums.length;
  const maxProduct1 = nums[n - 1] * nums[n - 2] * nums[n - 3];
  const maxProduct2 = nums[0] * nums[1] * nums[n - 1];
  return Math.max(maxProduct1, maxProduct2);
}

// Example:
const nums = [1, 2, 3];
const result = maximumProduct(nums);
console.log(result); // Output: 6

```

<hr/>

💡 **Question-6:** Given an array of integers nums which is sorted in ascending order, and an integer target,
write a function to search target in nums. If target exists, then return its index. Otherwise,
return -1.

You must write an algorithm with O(log n) runtime complexity.

Example: Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4

💬 **Solution-6:**

```js
function search(nums, target) {
  function binarySearch(start, end) {
    if (start > end) {
      return -1;
    }

    const mid = Math.floor((start + end) / 2);

    if (nums[mid] === target) {
      return mid;
    } else if (nums[mid] > target) {
      return binarySearch(start, mid - 1);
    } else {
      return binarySearch(mid + 1, end);
    }
  }

  return binarySearch(0, nums.length - 1);
}

// Example:
const nums = [-1, 0, 3, 5, 9, 12];
const target = 9;
const result = search(nums, target);
console.log(result); // Output: 4

```

<hr/>

💡 **Question-7:** An array is monotonic if it is either monotone increasing or monotone decreasing.

An array nums is monotone increasing if for all i <= j, nums[i] <= nums[j]. An array nums is
monotone decreasing if for all i <= j, nums[i] >= nums[j].

Given an integer array nums, return true if the given array is monotonic, or false otherwise.
Example:
Input: nums = [1,2,2,3]
Output: true

💬 **Solution-7:**

```js
function isMonotonic(nums) {
  let isIncreasing = true;
  let isDecreasing = true;

  for (let i = 1; i < nums.length; i++) {
    if (nums[i] < nums[i - 1]) {
      isIncreasing = false;
    }
    if (nums[i] > nums[i - 1]) {
      isDecreasing = false;
    }
  }
  return isIncreasing || isDecreasing;
}

// Example:
const nums = [1, 2, 2, 3];
const result = isMonotonic(nums);
console.log(result); // Output: true

```

<hr/>

💡 **Question-8:** You are given an integer array nums and an integer k.

In one operation, you can choose any index i where 0 <= i < nums.length and change nums[i] to nums[i] + x where x is an integer from the range [-k, k]. You can apply this operation at most once for each index i.

The score of nums is the difference between the maximum and minimum elements in nums.
Return the minimum score of nums after applying the mentioned operation at most once for each index in it.
Example:
Input: nums = [1], k = 0
Output: 0

💬 **Solution-8:**

```js
function minimumDifference(nums, k) {
  let minVal = Number.MAX_SAFE_INTEGER;
  let maxVal = Number.MIN_SAFE_INTEGER;

  for (let i = 0; i < nums.length; i++) {
    minVal = Math.min(minVal, nums[i]);
    maxVal = Math.max(maxVal, nums[i]);
  }
  if (minVal >= maxVal) {
    return 0;
  }

  const minScore = maxVal - k;
  const maxScore = minVal + k;
  return Math.min(minScore, maxVal - minVal);
}

// Example:
const nums = [1];
const k = 0;
const result = minimumDifference(nums, k);
console.log(result); // Output: 0

```

<hr/>

