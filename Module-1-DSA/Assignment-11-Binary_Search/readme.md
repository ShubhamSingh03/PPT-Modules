# Assignment-11 Questions & Solutions

💡 **Question-1:** Given a non-negative integer `x`, return the square root of `x` rounded down to the nearest integer. The returned integer should be non-negative as well.

You must not use any built-in exponent function or operator.

- For example, do not use `pow(x, 0.5)` in c++ or `x ** 0.5` in python.

Example 1:
```
Input: x = 4
Output: 2
Explanation: The square root of 4 is 2, so we return 2.
```

Example 2:
```
Input: x = 8
Output: 2
Explanation: The square root of 8 is 2.82842..., and since we round it down to the nearest integer, 2 is returned.
```

💬 **Solution-1:**

```js
function mySqrt(x) {
  if (x === 0) {
    return 0;
  }

  let left = 1;
  let right = Math.floor(x / 2) + 1;

  while (left <= right) {
    const mid = Math.floor((left + right) / 2);
    const square = mid * mid;

    if (square === x) {
      return mid;
    } else if (square < x) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }
  return right;
}

// Example:
console.log(mySqrt(4)); // Output: 2
console.log(mySqrt(8)); // Output: 2

```

<hr/>

💡 **Question-2:** A peak element is an element that is strictly greater than its neighbors.

Given a 0-indexed integer array `nums`, find a peak element, and return its index. If the array contains multiple peaks, return the index to any of the peaks.

You may imagine that `nums[-1] = nums[n] = -∞`. In other words, an element is always considered to be strictly greater than a neighbor that is outside the array.

You must write an algorithm that runs in `O(log n)` time.

Example 1:
```
Input: nums = [1,2,3,1]
Output: 2
Explanation: 3 is a peak element and your function should return the index number 2.
```

Example 2:
```
Input: nums = [1,2,1,3,5,6,4]
Output: 5
Explanation: Your function can return either index number 1 where the peak element is 2, or index number 5 where the peak element is 6.
```

💬 **Solution-2:**

```js
function findPeakElement(nums) {
  let left = 0;
  let right = nums.length - 1;

  while (left < right) {
    const mid = left + Math.floor((right - left) / 2);

    if (nums[mid] > nums[mid + 1] && nums[mid] > nums[mid - 1]) {
      return mid;
    } else if (nums[mid] < nums[mid + 1]) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }
  return nums[left] > nums[right] ? left : right;
}

// Example:
console.log(findPeakElement([1, 2, 3, 1])); // Output: 2
console.log(findPeakElement([1, 2, 1, 3, 5, 6, 4])); // Output: 5

```

<hr/>

💡 **Question-3:** Given an array `nums` containing `n` distinct numbers in the range `[0, n]`, return the only number in the range that is missing from the array.

Example 1:

```
Input: nums = [3,0,1]
Output: 2
Explanation: n = 3 since there are 3 numbers, so all numbers are in the range [0,3]. 2 is the missing number in the range since it does not appear in nums.
```

Example 2:

```
Input: nums = [0,1]
Output: 2
Explanation: n = 2 since there are 2 numbers, so all numbers are in the range [0,2]. 2 is the missing number in the range since it does not appear in nums.
```

Example 3:
```
Input: nums = [9,6,4,2,3,5,7,0,1]
Output: 8
Explanation: n = 9 since there are 9 numbers, so all numbers are in the range [0,9]. 8 is the missing number in the range since it does not appear in nums.
```

💬 **Solution-3:**

```js
function missingNumber(nums) {
  const n = nums.length;
  let expectedSum = (n * (n + 1)) / 2;

  for (const num of nums) {
    expectedSum -= num;
  }
  return expectedSum;
}

// Example:
console.log(missingNumber([3, 0, 1])); // Output: 2
console.log(missingNumber([0, 1])); // Output: 2
console.log(missingNumber([9, 6, 4, 2, 3, 5, 7, 0, 1])); // Output: 8

```

<hr/>

💡 **Question-4:** Given an array of integers `nums` containing `n + 1` integers where each integer is in the range `[1, n]` inclusive.

There is only one repeated number in `nums`, return this repeated number.

You must solve the problem without modifying the array `nums` and uses only constant extra space.

Example 1:

```
Input: nums = [1,3,4,2,2]
Output: 2
```

Example 2:
```
Input: nums = [3,1,3,4,2]
Output: 3
```

💬 **Solution-4:**

```js
function findDuplicate(nums) {
  let slow = nums[0];
  let fast = nums[0];
  do {
    slow = nums[slow];
    fast = nums[nums[fast]];
  } while (slow !== fast);

  slow = nums[0];
  while (slow !== fast) {
    slow = nums[slow];
    fast = nums[fast];
  }
  return slow;
}

// Example:
console.log(findDuplicate([1, 3, 4, 2, 2])); // Output: 2
console.log(findDuplicate([3, 1, 3, 4, 2])); // Output: 3

```

<hr/>

💡 **Question-5:** Given two integer arrays `nums1` and `nums2`, return an array of their intersection. Each element in the result must be unique and you may return the result in any order.

Example 1:

```
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2]
```

Example 2:
```
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [9,4]
Explanation: [4,9] is also accepted.
```

💬 **Solution-5:**

```js
function intersection(nums1, nums2) {
  const set = new Set();
  const intersection = [];

  for (const num of nums1) {
    set.add(num);
  }

  for (const num of nums2) {
    if (set.has(num)) {
      intersection.push(num);
      set.delete(num);
    }
  }
  return intersection;
}

// Example:
console.log(intersection([1, 2, 2, 1], [2, 2])); // Output: [2]
console.log(intersection([4, 9, 5], [9, 4, 9, 8, 4])); // Output: [9, 4]

```

<hr/>

💡 **Question-6:** Suppose an array of length `n` sorted in ascending order is rotated between `1` and `n` times. For example, the array `nums = [0,1,2,4,5,6,7]` might become:

- `[4,5,6,7,0,1,2]` if it was rotated `4` times.
- `[0,1,2,4,5,6,7]` if it was rotated `7` times.

Notice that rotating an array `[a[0], a[1], a[2], ..., a[n-1]]` 1 time results in the array `[a[n-1], a[0], a[1], a[2], ..., a[n-2]]`.

Given the sorted rotated array `nums` of unique elements, return the minimum element of this array.

You must write an algorithm that runs in `O(log n) time.`

Example 1:

```
Input: nums = [3,4,5,1,2]
Output: 1
Explanation: The original array was [1,2,3,4,5] rotated 3 times.
```

Example 2:

```
Input: nums = [4,5,6,7,0,1,2]
Output: 0
Explanation: The original array was [0,1,2,4,5,6,7] and it was rotated 4 times.
```

Example 3:
```
Input: nums = [11,13,15,17]
Output: 11
Explanation: The original array was [11,13,15,17] and it was rotated 4 times.
```

💬 **Solution-6:**

```js
function findMin(nums) {
  let left = 0;
  let right = nums.length - 1;

  while (left < right) {
    const mid = left + Math.floor((right - left) / 2);
    if (nums[mid] > nums[right]) {
      left = mid + 1;
    } else {
      right = mid;
    }
  }
  return nums[left];
}

// Example:
console.log(findMin([3, 4, 5, 1, 2])); // Output: 1
console.log(findMin([4, 5, 6, 7, 0, 1, 2])); // Output: 0
console.log(findMin([11, 13, 15, 17])); // Output: 11

```

<hr/>

💡 **Question-7:** Given an array of integers `nums` sorted in non-decreasing order, find the starting and ending position of a given `target` value.

If `target` is not found in the array, return `[-1, -1]`.

You must write an algorithm with `O(log n)` runtime complexity.

Example 1:

```
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]
```

Example 2:

```
Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]
```

Example 3:
```
Input: nums = [], target = 0
Output: [-1,-1]
```

💬 **Solution-7:**

```js
function searchRange(nums, target) {
  let left = 0;
  let right = nums.length - 1;

  // Finding the leftmost occurrence of the target
  while (left < right) {
    const mid = left + Math.floor((right - left) / 2);
    if (nums[mid] >= target) {
      right = mid;
    } else {
      left = mid + 1;
    }
  }

  if (left === nums.length || nums[left] !== target) {
    return [-1, -1];
  }

  // Finding the rightmost occurrence of the target
  right = nums.length - 1;
  while (left < right) {
    const mid = left + Math.floor((right - left + 1) / 2);
    if (nums[mid] > target) {
      right = mid - 1;
    } else {
      left = mid;
    }
  }
  return [left, right];
}

// Example:
console.log(searchRange([5, 7, 7, 8, 8, 10], 8)); // Output: [3, 4]
console.log(searchRange([5, 7, 7, 8, 8, 10], 6)); // Output: [-1, -1]
console.log(searchRange([], 0)); // Output: [-1, -1]

```

<hr/>

💡 **Question-8:** Given two integer arrays `nums1` and `nums2`, return an array of their intersection. Each element in the result must appear as many times as it shows in both arrays and you may return the result in any order.

Example 1:

```
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2,2]
```

Example 2:
```
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [4,9]
Explanation: [9,4] is also accepted.
```

💬 **Solution-8:**

```js
function intersect(nums1, nums2) {
  const map1 = new Map();
  const map2 = new Map();

  // Counting occurrences in nums1
  for (const num of nums1) {
    map1.set(num, (map1.get(num) || 0) + 1);
  }

  // Counting occurrences in nums2
  for (const num of nums2) {
    map2.set(num, (map2.get(num) || 0) + 1);
  }

  const result = [];
  // Finding the intersection
  for (const [num, count1] of map1) {
    if (map2.has(num)) {
      const count2 = map2.get(num);
      const commonCount = Math.min(count1, count2);
      for (let i = 0; i < commonCount; i++) {
        result.push(num);
      }
    }
  }
  return result;
}

// Example:
console.log(intersect([1, 2, 2, 1], [2, 2])); // Output: [2, 2]
console.log(intersect([4, 9, 5], [9, 4, 9, 8, 4])); // Output: [4, 9]

```

<hr/>