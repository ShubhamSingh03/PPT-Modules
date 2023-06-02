# Assignment-1 Questions & Solutions

💡 **Question-1:** Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

💬 **Solution-1:**

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

// Example:
const nums = [2, 7, 11, 15];
const target = 9;
const result = twoSum(nums, target);
console.log(result); // Output: [0, 1]

```

<hr/>

💡 **Question-2:** Given an integer array nums and an integer val, remove all occurrences of val in nums in-place. The order of the elements may be changed. Then return the number of elements in nums which are not equal to val.

Consider the number of elements in nums which are not equal to val be k, to get accepted, you need to do the following things:

- Change the array nums such that the first k elements of nums contain the elements which are not equal to val. The remaining elements of nums are not important as well as the size of nums.
- Return k.

Example :
Input: nums = [3,2,2,3], val = 3
Output: 2, nums = [2,2,_,_]

💬 **Solution-2:**

```js
function removeElement(nums, val) {
    let k = 0;
    for (let i = 0; i < nums.length; i++) {
        if (nums[i] !== val) {
            nums[k] = nums[i];
            k++;
        }
    }
    return k;
}

// Example:
const nums = [3, 2, 2, 3];
const val = 3;
const result = removeElement(nums, val);
console.log(result); // Output: 2 (nums = [2, 2])

```

<hr/>

💡 **Question-3:** Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with O(log n) runtime complexity.
Example: Input: nums = [1,3,5,6], target = 5 Output: 2

💬 **Solution-3:**

```js
function searchInsert(nums, target) {
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
    return left;
}

// Example:
const nums = [1, 3, 5, 6];
const target = 5;
const result = searchInsert(nums, target);
console.log(result); // Output: 2

```

<hr/>

💡 **Question-4:** You are given a large integer represented as an integer array digits, where each digits[i] is the ith digit of the integer. The digits are ordered from most significant to least significant in left-to-right order. The large integer does not contain any leading 0's.

Increment the large integer by one and return the resulting array of digits.
Example:
Input: digits = [1,2,3]
Output: [1,2,4]

💬 **Solution-4:**

```js
function plusOne(digits) {
    const n = digits.length;
    for (let i = n - 1; i >= 0; i--) {
        digits[i]++;
        if (digits[i] === 10) {
            digits[i] = 0;
        } else {
            return digits;
        }
    }
    digits.unshift(1);
    return digits;
}

// Example:
const digits = [1, 2, 3];
const result = plusOne(digits);
console.log(result); // Output: [1, 2, 4]

```

<hr/>


💡 **Question-5:** You are given two integer arrays nums1 and nums2, sorted in non-decreasing order, and two integers m and n, representing the number of elements in nums1 and nums2 respectively.

Merge nums1 and nums2 into a single array sorted in non-decreasing order.

The final sorted array should not be returned by the function, but instead be stored inside the array nums1. To accommodate this, nums1 has a length of m + n, where the first m elements denote the elements that should be merged, and the last n elements are set to 0 and should be ignored. nums2 has a length of n.

Example:
Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
Output: [1,2,2,3,5,6]

💬 **Solution-5:**

```js
function merge(nums1, m, nums2, n) {
    let p1 = m - 1;
    let p2 = n - 1;
    let p = m + n - 1;

    while (p1 >= 0 && p2 >= 0) {
        if (nums1[p1] > nums2[p2]) {
            nums1[p] = nums1[p1];
            p1--;
        } else {
            nums1[p] = nums2[p2];
            p2--;
        }
        p--;
    }
    while (p2 >= 0) {
        nums1[p] = nums2[p2];
        p2--;
        p--;
    }
}

// Example:
const nums1 = [1, 2, 3, 0, 0, 0];
const m = 3;
const nums2 = [2, 5, 6];
const n = 3;

merge(nums1, m, nums2, n);
console.log(nums1); // Output: [1, 2, 2, 3, 5, 6]

```

<hr/>

💡 **Question-6:**  Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.
Example:
Input: nums = [1,2,3,1]
Output: true

💬 **Solution-6:**

```js
function containsDuplicate(nums) {
    const set = new Set();
    for (let i = 0; i < nums.length; i++) {
        if (set.has(nums[i])) {
            return true;
        }
        set.add(nums[i]);
    }
    return false;
}

// Example:
const nums = [1, 2, 3, 1];
const result = containsDuplicate(nums);
console.log(result); // Output: true

```

<hr/>

💡 **Question-7:** Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the nonzero elements.

Note that you must do this in-place without making a copy of the array.
Example:
Input: nums = [0,1,0,3,12]
Output: [1,3,12,0,0]

💬 **Solution-7:**

```js
function moveZeroes(nums) {
    let j = 0;
    for (let i = 0; i < nums.length; i++) {
        if (nums[i] !== 0) {
            nums[j] = nums[i];
            j++;
        }
    }
    while (j < nums.length) {
        nums[j] = 0;
        j++;
    }
}

// Example:
const nums = [0, 1, 0, 3, 12];
moveZeroes(nums);
console.log(nums); // Output: [1, 3, 12, 0, 0]

```

<hr/>

💡 **Question-8:** You have a set of integers s, which originally contains all the numbers from 1 to n. Unfortunately, due to some error, one of the numbers in s got duplicated to another number in the set, which results in repetition of one number and loss of another number.

You are given an integer array nums representing the data status of this set after the error.

Find the number that occurs twice and the number that is missing and return them in the form of an array.
Example:
Input: nums = [1,2,2,4]
Output: [2,3]

💬 **Solution-8:**

```js
function findErrorNums(nums) {
    const n = nums.length;
    const set = new Set();
    let duplicate = -1;
    let expectedSum = (n * (n + 1)) / 2;
    let actualSum = 0;

    for (let i = 0; i < n; i++) {
        if (set.has(nums[i])) {
            duplicate = nums[i];
        }
        set.add(nums[i]);
        actualSum += nums[i];
    }
    const missing = expectedSum - (actualSum - duplicate);
    return [duplicate, missing];
}

// Example:
const nums = [1, 2, 2, 4];
const result = findErrorNums(nums);
console.log(result); // Output: [2, 3]

```
<hr/>