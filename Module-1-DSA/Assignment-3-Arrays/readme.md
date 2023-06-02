# Assignment-3 Questions & Solutions

💡 **Question-1:** Given an integer array nums of length n and an integer target, find three integers
in nums such that the sum is closest to the target.
Return the sum of the three integers.

You may assume that each input would have exactly one solution.

Example:
Input: nums = [-1,2,1,-4], target = 1
Output: 2


💬 **Solution-1:**

```js
function threeSumClosest(nums, target) {
    nums.sort((a, b) => a - b);
    let closestSum = Infinity;

    for (let i = 0; i < nums.length - 2; i++) {
        let left = i + 1;
        let right = nums.length - 1;

        while (left < right) {
            const currentSum = nums[i] + nums[left] + nums[right];

            if (Math.abs(currentSum - target) < Math.abs(closestSum - target)) {
                closestSum = currentSum;
            }
            if (currentSum > target) {
                right--;
            } else if (currentSum < target) {
                left++;
            } else {
                return currentSum;
            }
        }
    }
    return closestSum;
}

// Example:
const nums = [-1, 2, 1, -4];
const target = 1;
const result = threeSumClosest(nums, target);
console.log(result); // Output: 2

```

<hr/>

💡 **Question-2:** Given an array nums of n integers, return an array of all the unique quadruplets [nums[a], nums[b], nums[c], nums[d]] such that:
- 0 <= a, b, c, d < n
- a, b, c, and d are distinct.
- nums[a] + nums[b] + nums[c] + nums[d] == target

You may return the answer in any order.

Example:
Input: nums = [1,0,-1,0,-2,2], target = 0
Output: [[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]

💬 **Solution-2:**

```js
function fourSum(nums, target) {
    nums.sort((a, b) => a - b);
    const result = [];

    for (let i = 0; i < nums.length - 3; i++) {
        if (i > 0 && nums[i] === nums[i - 1]) {
            continue;
        }

        for (let j = i + 1; j < nums.length - 2; j++) {
            if (j > i + 1 && nums[j] === nums[j - 1]) {
                continue;
            }

            let left = j + 1;
            let right = nums.length - 1;

            while (left < right) {
                const currentSum = nums[i] + nums[j] + nums[left] + nums[right];

                if (currentSum === target) {
                    result.push([nums[i], nums[j], nums[left], nums[right]]);

                    while (left < right && nums[left] === nums[left + 1]) {
                        left++;
                    }
                    left++;

                    while (left < right && nums[right] === nums[right - 1]) {
                        right--;
                    }
                    right--;
                } else if (currentSum < target) {
                    left++;
                } else {
                    right--;
                }
            }
        }
    }
    return result;
}

// Example:
const nums = [1, 0, -1, 0, -2, 2];
const target = 0;
const result = fourSum(nums, target);
console.log(result);
// Output: [[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]

```

<hr/>

💡 **Question-3:** A permutation of an array of integers is an arrangement of its members into a
sequence or linear order.

For example, for arr = [1,2,3], the following are all the permutations of arr:
[1,2,3], [1,3,2], [2, 1, 3], [2, 3, 1], [3,1,2], [3,2,1].

The next permutation of an array of integers is the next lexicographically greater
permutation of its integer. More formally, if all the permutations of the array are
sorted in one container according to their lexicographical order, then the next
permutation of that array is the permutation that follows it in the sorted container.

If such an arrangement is not possible, the array must be rearranged as the
lowest possible order (i.e., sorted in ascending order).

- For example, the next permutation of arr = [1,2,3] is [1,3,2].
- Similarly, the next permutation of arr = [2,3,1] is [3,1,2].
- While the next permutation of arr = [3,2,1] is [1,2,3] because [3,2,1] does not have a lexicographical larger rearrangement.

Given an array of integers nums, find the next permutation of nums.
The replacement must be in place and use only constant extra memory.

Example:
Input: nums = [1,2,3]
Output: [1,3,2]

💬 **Solution-3:**

```js
function nextPermutation(nums) {
    let i = nums.length - 2;
    while (i >= 0 && nums[i] >= nums[i + 1]) {
        i--;
    }

    if (i >= 0) {
        let j = nums.length - 1;
        // Find the smallest element greater than nums[i]
        while (j >= 0 && nums[j] <= nums[i]) {
            j--;
        }
        swap(nums, i, j);
    }
    reverse(nums, i + 1);
}

function swap(nums, i, j) {
    const temp = nums[i];
    nums[i] = nums[j];
    nums[j] = temp;
}

function reverse(nums, start) {
    let i = start;
    let j = nums.length - 1;
    while (i < j) {
        swap(nums, i, j);
        i++;
        j--;
    }
}

// Example:
const nums = [1, 2, 3];
nextPermutation(nums);
console.log(nums); // Output: [1, 3, 2]

```

<hr/>

💡 **Question-4:** Given a sorted array of distinct integers and a target value, return the index if the
target is found. If not, return the index where it would be if it were inserted in
order.

You must write an algorithm with O(log n) runtime complexity.

Example:
Input: nums = [1,3,5,6], target = 5
Output: 2

💬 **Solution-4:**

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
const index = searchInsert(nums, target);
console.log(index); // Output: 2

```

<hr/>

💡 **Question-5:** You are given a large integer represented as an integer array digits, where each
digits[i] is the ith digit of the integer. The digits are ordered from most significant to least significant in left-to-right order. The large integer does not contain any
leading 0's.

Increment the large integer by one and return the resulting array of digits.

Example:
Input: digits = [1,2,3]
Output: [1,2,4]

💬 **Solution-5:**

```js
function plusOne(digits) {
    const n = digits.length;
    for (let i = n - 1; i >= 0; i--) {
        if (digits[i] < 9) {
            digits[i]++;
            return digits;
        }
        digits[i] = 0;
    }
    // If all digits are 9, add a new leading 1
    digits.unshift(1);
    return digits;
}

// Example:
const digits = [1, 2, 3];
const result = plusOne(digits);
console.log(result); // Output: [1, 2, 4]

```

<hr/>

💡 **Question-6:** Given a non-empty array of integers nums, every element appears twice except
for one. Find that single one.

You must implement a solution with a linear runtime complexity and use only constant extra space. 
Example:
Input: nums = [2,2,1]
Output: 1

💬 **Solution-6:**

```js
function singleNumber(nums) {
    let result = 0;
    for (let i = 0; i < nums.length; i++) {
        result ^= nums[i];
    }
    return result;
}

// Example:
const nums = [2, 2, 1];
const result = singleNumber(nums);
console.log(result); // Output: 1

```

<hr/>

💡 **Question-7:** You are given an inclusive range [lower, upper] and a sorted unique integer array nums, where all elements are within the inclusive range.

A number x is considered missing if x is in the range [lower, upper] and x is not in nums.

Return the shortest sorted list of ranges that exactly covers all the missing numbers. That is, no element of nums is included in any of the ranges, and each missing number is covered by one of the ranges.

Example:
Input: nums = [0,1,3,50,75], lower = 0, upper = 99
Output: [[2,2],[4,49],[51,74],[76,99]]

💬 **Solution-7:**

```js
function findMissingRanges(nums, lower, upper) {
    const result = [];
    let prev = lower - 1;
    for (let i = 0; i <= nums.length; i++) {
        let curr = (i < nums.length) ? nums[i] : upper + 1;
        if (curr - prev > 1) {
            result.push(formatRange(prev + 1, curr - 1));
        }
        prev = curr;
    }
    return result;
}

function formatRange(start, end) {
    return (start === end) ? `${start}` : `${start}->${end}`;
}

// Example:
const nums = [0, 1, 3, 50, 75];
const lower = 0;
const upper = 99;
const result = findMissingRanges(nums, lower, upper);
console.log(result); // Output: [[2,2],[4,49],[51,74],[76,99]]

```

<hr/>

💡 **Question-8:** Given an array of meeting time intervals where intervals[i] = [starti, endi], determine if a person could attend all meetings.

Example:
Input: intervals = [[0,30],[5,10],[15,20]]
Output: false

💬 **Solution-8:**

```js
function canAttendMeetings(intervals) {
    intervals.sort((a, b) => a[0] - b[0]);
    for (let i = 1; i < intervals.length; i++) {
        if (intervals[i][0] < intervals[i - 1][1]) {
            return false;
        }
    }
    return true;
}

// Example:
const intervals = [[0, 30], [5, 10], [15, 20]];
const result = canAttendMeetings(intervals);
console.log(result); // Output: false

```

<hr/>