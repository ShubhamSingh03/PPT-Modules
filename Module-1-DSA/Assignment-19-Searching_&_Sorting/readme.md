# Assignment-19 Questions & Solutions

💡 **Question-1:**  **Merge k Sorted Lists**

You are given an array of `k` linked-lists `lists`, each linked-list is sorted in ascending order.

*Merge all the linked-lists into one sorted linked-list and return it.*

Examples:

```
Input: lists = [[1,4,5],[1,3,4],[2,6]]
Output: [1,1,2,3,4,4,5,6]
Explanation: The linked-lists are:
[
  1->4->5,
  1->3->4,
  2->6
]
merging them into one sorted list:
1->1->2->3->4->4->5->6

Input: lists = []
Output: []

Input: lists = [[]]
Output: []
```

Constraints:

- `k == lists.length`
- `0 <= k <= 10000`
- `0 <= lists[i].length <= 500`
- `-10000 <= lists[i][j] <= 10000`
- `lists[i]` is sorted in **ascending order**.
- The sum of `lists[i].length` will not exceed `10000`.


💬 **Solution-1:**

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
// merging two sorted linked lists.
function mergeTwoLists(l1, l2) {
  if (!l1) return l2;
  if (!l2) return l1;

  if (l1.val < l2.val) {
    l1.next = mergeTwoLists(l1.next, l2);
    return l1;
  } else {
    l2.next = mergeTwoLists(l1, l2.next);
    return l2;
  }
}

// merging all the linked lists into one sorted linked list.
function mergeKLists(lists) {
  if (lists.length === 0) return null;

  let interval = 1;
  const n = lists.length;

  while (interval < n) {
    for (let i = 0; i < n - interval; i += interval * 2) {
      lists[i] = mergeTwoLists(lists[i], lists[i + interval]);
    }
    interval *= 2;
  }
  return lists[0];
}

// creating linked list nodes
function ListNode(val, next) {
  this.val = val === undefined ? 0 : val;
  this.next = next === undefined ? null : next;
}

// creating linked lists
const list1 = new ListNode(1);
list1.next = new ListNode(4);
list1.next.next = new ListNode(5);

const list2 = new ListNode(1);
list2.next = new ListNode(3);
list2.next.next = new ListNode(4);

const list3 = new ListNode(2);
list3.next = new ListNode(6);

// constructing the array of linked lists
const lists = [list1, list2, list3];

// merging the linked lists
const result = mergeKLists(lists);

// printing the merged linked list
let currentNode = result;
const mergedList = [];
while (currentNode) {
  mergedList.push(currentNode.val);
  currentNode = currentNode.next;
}
console.log(mergedList); // Output: [1, 1, 2, 3, 4, 4, 5, 6]
```

<hr/>

💡 **Question-2:** **Count of Smaller Numbers After Self**

Given an integer array `nums`, return *an integer array* `counts` *where* `counts[i]` *is the number of smaller elements to the right of* `nums[i]`.

Examples:

```
Input: nums = [5,2,6,1]
Output: [2,1,1,0]
Explanation:
To the right of 5 there are2 smaller elements (2 and 1).
To the right of 2 there is only1 smaller element (1).
To the right of 6 there is1 smaller element (1).
To the right of 1 there is0 smaller element.

Input: nums = [-1]
Output: [0]

Input: nums = [-1,-1]
Output: [0,0]
```

Constraints:

- `1 <= nums.length <= 100000`
- `-10000 <= nums[i] <= 10000`


💬 **Solution-2:**

```js
// returning an array where counts[i] is the number of smaller elements to the right of nums[i].
function countSmaller(nums) {
  const counts = new Array(nums.length).fill(0);
  const indexedNums = nums.map((value, index) => [value, index]);
  mergeSort(indexedNums, counts);
  return counts;
}

// performing Merge Sort and count the number of smaller elements to the right.
function mergeSort(indexedNums, counts) {
  if (indexedNums.length <= 1) {
    return indexedNums;
  }

  const mid = Math.floor(indexedNums.length / 2);
  const left = mergeSort(indexedNums.slice(0, mid), counts);
  const right = mergeSort(indexedNums.slice(mid), counts);
  return merge(left, right, counts);
}

// merging two sorted subarrays and count the number of smaller elements to the right.
function merge(left, right, counts) {
  const merged = [];
  let count = 0;
  let i = 0;
  let j = 0;

  while (i < left.length || j < right.length) {
    if (j === right.length || (i < left.length && left[i][0] <= right[j][0])) {
      merged.push(left[i]);
      counts[left[i][1]] += count;
      i++;
    } else {
      merged.push(right[j]);
      count++;
      j++;
    }
  }
  return merged;
}

// Example:
const nums = [5, 2, 6, 1];
const counts = countSmaller(nums);
console.log(counts); // Output: [2, 1, 1, 0]
```

<hr/>

💡 **Question-3:** **Sort an Array**

Given an array of integers `nums`, sort the array in ascending order and return it.

You must solve the problem **without using any built-in** functions in `O(nlog(n))` time complexity and with the smallest space complexity possible.

Examples:

```
Input: nums = [5,2,3,1]
Output: [1,2,3,5]
Explanation: After sorting the array, the positions of some numbers are not changed (for example, 2 and 3), while the positions of other numbers are changed (for example, 1 and 5).

Input: nums = [5,1,1,2,0,0]
Output: [0,0,1,1,2,5]
Explanation: Note that the values of nums are not necessairly unique.
```

Constraints:

- `1 <= nums.length <= 5 * 10000`
- `-5 * 104 <= nums[i] <= 5 * 10000`


💬 **Solution-3:**

```js
// sorting the array in ascending order using QuickSort algorithm.
function quickSort(nums, low, high) {
  if (low < high) {
    const pivotIndex = partition(nums, low, high);
    quickSort(nums, low, pivotIndex - 1);
    quickSort(nums, pivotIndex + 1, high);
  }
}

// partitioning the array and return the index of the pivot element.
function partition(nums, low, high) {
  const pivot = nums[high];
  let i = low - 1;

  for (let j = low; j < high; j++) {
    if (nums[j] <= pivot) {
      i++;
      swap(nums, i, j);
    }
  }
  swap(nums, i + 1, high);
  return i + 1;
}

// swaping the elements at the given indices in the array.
function swap(nums, i, j) {
  const temp = nums[i];
  nums[i] = nums[j];
  nums[j] = temp;
}

// Example:
const nums = [5, 2, 3, 1];
quickSort(nums, 0, nums.length - 1);
console.log(nums); // Output: [1, 2, 3, 5]
```

<hr/>

💡 **Question-4:**  **Move all zeroes to end of array**

Given an array of random numbers, Push all the zero’s of a given array to the end of the array. For example, if the given arrays is {1, 9, 8, 4, 0, 0, 2, 7, 0, 6, 0}, it should be changed to {1, 9, 8, 4, 2, 7, 6, 0, 0, 0, 0}. The order of all other elements should be same. Expected time complexity is O(n) and extra space is O(1).

Examples:

```
Input :  arr[] = {1, 2, 0, 4, 3, 0, 5, 0};
Output : arr[] = {1, 2, 4, 3, 5, 0, 0, 0};

Input : arr[]  = {1, 2, 0, 0, 0, 3, 6};
Output : arr[] = {1, 2, 3, 6, 0, 0, 0};
```

💬 **Solution-4:**

```js
function pushZeroesToEnd(arr) {
  let i = 0; // pointer for non-zero elements

  // moving non-zero elements towards the beginning
  for (let j = 0; j < arr.length; j++) {
    if (arr[j] !== 0) {
      arr[i] = arr[j];
      i++;
    }
  }

  // filling the remaining elements with zeroes
  while (i < arr.length) {
    arr[i] = 0;
    i++;
  }
}

// Example:
const arr = [1, 2, 0, 4, 3, 0, 5, 0];
pushZeroesToEnd(arr);
console.log(arr); // Output: [1, 2, 4, 3, 5, 0, 0, 0]
```

<hr/>

💡 **Question-5:** **Rearrange array in alternating positive & negative items with O(1) extra space**

Given an **array of positive** and **negative numbers**, arrange them in an **alternate** fashion such that every positive number is followed by a negative and vice-versa maintaining the **order of appearance**. The number of positive and negative numbers need not be equal. If there are more positive numbers they appear at the end of the array. If there are more negative numbers, they too appear at the end of the array.

Examples:

```
Input:  arr[] = {1, 2, 3, -4, -1, 4}
Output: arr[] = {-4, 1, -1, 2, 3, 4}

Input:  arr[] = {-5, -2, 5, 2, 4, 7, 1, 8, 0, -8}
Output: arr[] = {-5, 5, -2, 2, -8, 4, 7, 1, 8, 0}
```


💬 **Solution-5:**

```js
function alternatePositiveNegative(arr) {
  let i = 0; // pointer for positive numbers

  while (i < arr.length) {
    // finding the next negative number
    let j = i + 1;
    while (j < arr.length && arr[j] >= 0) {
      j++;
    }

    // swaping positive and negative numbers
    if (j < arr.length) {
      const temp = arr[j];
      for (let k = j; k > i; k--) {
        arr[k] = arr[k - 1];
      }
      arr[i] = temp;
    }
    // incrementing the pointer for positive numbers
    i += 2;
  }
}

// Example:
const arr = [1, 2, 3, -4, -1, 4];
alternatePositiveNegative(arr);
console.log(arr); // Output: [-4, 1, -1, 2, 3, 4]
```

<hr/>

💡 **Question-6:** **Merge two sorted arrays**

Given two sorted arrays, the task is to merge them in a sorted manner.

Examples:

```
Input: arr1[] = { 1, 3, 4, 5}, arr2[] = {2, 4, 6, 8} 
Output: arr3[] = {1, 2, 3, 4, 4, 5, 6, 8}

Input: arr1[] = { 5, 8, 9}, arr2[] = {4, 7, 8}
Output: arr3[] = {4, 5, 7, 8, 8, 9}
```


💬 **Solution-6:**

```js
function mergeSortedArrays(arr1, arr2) {
  const merged = [];
  let i = 0; // pointer for arr1
  let j = 0; // pointer for arr2

  while (i < arr1.length && j < arr2.length) {
    if (arr1[i] <= arr2[j]) {
      merged.push(arr1[i]);
      i++;
    } else {
      merged.push(arr2[j]);
      j++;
    }
  }

  // adding remaining elements from arr1, if any
  while (i < arr1.length) {
    merged.push(arr1[i]);
    i++;
  }

  // adding remaining elements from arr2, if any
  while (j < arr2.length) {
    merged.push(arr2[j]);
    j++;
  }
  return merged;
}

// Example:
const arr1 = [1, 3, 4, 5];
const arr2 = [2, 4, 6, 8];

const result = mergeSortedArrays(arr1, arr2);
console.log(result); // Output: [1, 2, 3, 4, 4, 5, 6, 8]
```

<hr/>

💡 **Question-7:** **Intersection of Two Arrays**

Given two integer arrays `nums1` and `nums2`, return an array of their intersection. Each element in the result must be **unique** and you may return the result in **any order**.

Examples:

```
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2]

Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [9,4]
Explanation: [4,9] is also accepted.
```

Constraints:

- `1 <= nums1.length, nums2.length <= 1000`
- `0 <= nums1[i], nums2[i] <= 1000`


💬 **Solution-7:**

```js
function intersection(nums1, nums2) {
  const set1 = new Set(nums1);
  const set2 = new Set(nums2);
  const result = [];

  // finding common elements in the two sets
  for (const num of set1) {
    if (set2.has(num)) {
      result.push(num);
    }
  }
  return result;
}

// Example:
const nums1 = [1, 2, 2, 1];
const nums2 = [2, 2];

const result = intersection(nums1, nums2);
console.log(result); // Output: [2]
```

<hr/>

💡 **Question-8:** **Intersection of Two Arrays II**

Given two integer arrays `nums1` and `nums2`, return *an array of their intersection*. Each element in the result must appear as many times as it shows in both arrays and you may return the result in **any order**.

Examples:

```
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2,2]

Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [4,9]
Explanation: [9,4] is also accepted.
```

Constraints:

- `1 <= nums1.length, nums2.length <= 1000`
- `0 <= nums1[i], nums2[i] <= 1000`


💬 **Solution-8:**

```js
function intersect(nums1, nums2) {
  const map = new Map();
  const result = [];

  // storing the frequency of elements in nums1
  for (const num of nums1) {
    map.set(num, (map.get(num) || 0) + 1);
  }

  // iterating over nums2 and find common elements
  for (const num of nums2) {
    if (map.has(num) && map.get(num) > 0) {
      result.push(num);
      map.set(num, map.get(num) - 1);
    }
  }
  return result;
}

// Example:
const nums1 = [1, 2, 2, 1];
const nums2 = [2, 2];

const result = intersect(nums1, nums2);
console.log(result); // Output: [2, 2]
```

<hr/>