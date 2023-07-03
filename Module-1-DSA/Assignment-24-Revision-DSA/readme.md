# Assignment-24 Questions & Solutions

💡 **Question-1:** **Roman to Integer**

Roman numerals are represented by seven different symbols: `I`, `V`, `X`, `L`, `C`, `D` and `M`.

```
SymbolValue
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

For example, `2` is written as `II` in Roman numeral, just two ones added together. `12` is written as `XII`, which is simply `X + II`. The number `27` is written as `XXVII`, which is `XX + V + II`.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not `IIII`. Instead, the number four is written as `IV`. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as `IX`. There are six instances where subtraction is used:

- `I` can be placed before `V` (5) and `X` (10) to make 4 and 9.
- `X` can be placed before `L` (50) and `C` (100) to make 40 and 90.
- `C` can be placed before `D` (500) and `M` (1000) to make 400 and 900.

Given a roman numeral, convert it to an integer.

Example 1:

```
Input: s = "III"
Output: 3
Explanation: III = 3.
```

Example 2:

```
Input: s = "LVIII"
Output: 58
Explanation: L = 50, V= 5, III = 3.
```

Constraints:

- `1 <= s.length <= 15`
- `s` contains only the characters `('I', 'V', 'X', 'L', 'C', 'D', 'M')`.
- It is **guaranteed** that `s` is a valid roman numeral in the range `[1, 3999]`.

💬 **Solution-1:**

```js
function romanToInt(s) {
  const romanValues = {
    I: 1,
    V: 5,
    X: 10,
    L: 50,
    C: 100,
    D: 500,
    M: 1000
  };

  let result = 0;

  for (let i = 0; i < s.length; i++) {
    const currentSymbol = s[i];
    const currentValue = romanValues[currentSymbol];
    const nextSymbol = s[i + 1];
    const nextValue = romanValues[nextSymbol];

    if (nextValue && nextValue > currentValue) {
      result += nextValue - currentValue;
      i++; // Skip the next symbol since it has been accounted for
    } else {
      result += currentValue;
    }
  }
  return result;
}

// Example:
console.log(romanToInt("III")); // Output: 3
console.log(romanToInt("LVIII")); // Output: 58
```

<hr/>

💡 **Question-2:** **Longest Substring Without Repeating Characters**

Given a string `s`, find the length of the **longest substring** without repeating characters.

Example 1:

```
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```

Example 2:

```
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```

Example 3:

```
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

Constraints:

- `0 <= s.length <= 50000`
- `s` consists of English letters, digits, symbols and spaces.

💬 **Solution-2:**

```js
function lengthOfLongestSubstring(s) {
  const charSet = new Set();
  let maxLength = 0;
  let left = 0;
  let right = 0;

  while (right < s.length) {
    if (!charSet.has(s[right])) {
      charSet.add(s[right]);
      maxLength = Math.max(maxLength, charSet.size);
      right++;
    } else {
      charSet.delete(s[left]);
      left++;
    }
  }
  return maxLength;
}

// Example:
console.log(lengthOfLongestSubstring("abcabcbb")); // Output: 3
console.log(lengthOfLongestSubstring("bbbbb")); // Output: 1
console.log(lengthOfLongestSubstring("pwwkew")); // Output: 3
```

<hr/>

💡 **Question-3:** **Majority Element**

Given an array `nums` of size `n`, return *the majority element*.

The majority element is the element that appears more than `⌊n / 2⌋` times. You may assume that the majority element always exists in the array.

Example 1:

```
Input: nums = [3,2,3]
Output: 3
```

Example 2:

```
Input: nums = [2,2,1,1,1,2,2]
Output: 2
```

Constraints:

- `n == nums.length`
- `1 <= n <= 5 * 10^4`
- `-10^9 <= nums[i] <= 10^9`

💬 **Solution-3:**

```js
function majorityElement(nums) {
  let majority = nums[0];
  let count = 1;

  for (let i = 1; i < nums.length; i++) {
    if (nums[i] === majority) {
      count++;
    } else {
      count--;
      if (count === 0) {
        majority = nums[i];
        count = 1;
      }
    }
  }
  return majority;
}

// Example:
console.log(majorityElement([3, 2, 3])); // Output: 3
console.log(majorityElement([2, 2, 1, 1, 1, 2, 2])); // Output: 2
```

<hr/>

💡 **Question-4:** **Group Anagram**

Given an array of strings `strs`, group **the anagrams** together. You can return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

Example 1:

```
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
```

Example 2:

```
Input: strs = [""]
Output: [[""]]
```

Example 3:

```
Input: strs = ["a"]
Output: [["a"]]
```

Constraints:

- `1 <= strs.length <= 10000`
- `0 <= strs[i].length <= 100`
- `strs[i]` consists of lowercase English letters.

💬 **Solution-4:**

```js
function groupAnagrams(strs) {
  const map = {};

  for (let str of strs) {
    const sortedStr = str.split("").sort().join("");

    if (map[sortedStr]) {
      map[sortedStr].push(str);
    } else {
      map[sortedStr] = [str];
    }
  }
  return Object.values(map);
}

// Example:
console.log(groupAnagrams(["eat", "tea", "tan", "ate", "nat", "bat"]));
// Output: [["eat", "tea", "ate"], ["tan", "nat"], ["bat"]]

console.log(groupAnagrams([""]));
// Output: [[""]]

console.log(groupAnagrams(["a"]));
// Output: [["a"]]
```

<hr/>

💡 **Question-5:** **Ugly Numbers**

An **ugly number** is a positive integer whose prime factors are limited to `2`, `3`, and `5`.

Given an integer `n`, return *the* `nth` ***ugly number***.

Example 1:

```
Input: n = 10
Output: 12
Explanation: [1, 2, 3, 4, 5, 6, 8, 9, 10, 12] is the sequence of the first 10 ugly numbers.
```

Example 2:

```
Input: n = 1
Output: 1
Explanation: 1 has no prime factors, therefore all of its prime factors are limited to 2, 3, and 5.
```

Constraints:

- `1 <= n <= 1690`

💬 **Solution-5:**

```js
function nthUglyNumber(n) {
  const uglyNumbers = [1];
  let i2 = 0,
    i3 = 0,
    i5 = 0;

  for (let i = 1; i < n; i++) {
    const nextUgly = Math.min(
      uglyNumbers[i2] * 2,
      uglyNumbers[i3] * 3,
      uglyNumbers[i5] * 5
    );
    uglyNumbers.push(nextUgly);

    if (nextUgly === uglyNumbers[i2] * 2) {
      i2++;
    }
    if (nextUgly === uglyNumbers[i3] * 3) {
      i3++;
    }
    if (nextUgly === uglyNumbers[i5] * 5) {
      i5++;
    }
  }
  return uglyNumbers[n - 1];
}

// Example:
console.log(nthUglyNumber(10)); // Output: 12
console.log(nthUglyNumber(1)); // Output: 1
```

<hr/>

💡 **Question-6:** **Top K Frequent Words**

Given an array of strings `words` and an integer `k`, return *the* `k` *most frequent strings*.

Return the answer **sorted** by **the frequency** from highest to lowest. Sort the words with the same frequency by their **lexicographical order**.

Example 1:

```
Input: words = ["i","love","leetcode","i","love","coding"], k = 2
Output: ["i","love"]
Explanation: "i" and "love" are the two most frequent words.
Note that "i" comes before "love" due to a lower alphabetical order.
```

Example 2:

```
Input: words = ["the","day","is","sunny","the","the","the","sunny","is","is"], k = 4
Output: ["the","is","sunny","day"]
Explanation: "the", "is", "sunny" and "day" are the four most frequent words, with the number of occurrence being 4, 3, 2 and 1 respectively.
```

Constraints:

- `1 <= words.length <= 500`
- `1 <= words[i].length <= 10`
- `words[i]` consists of lowercase English letters.
- `k` is in the range `[1, The number of **unique** words[i]]`

💬 **Solution-6:**

```js
function topKFrequent(words, k) {
  const freqMap = new Map();

  for (let word of words) {
    freqMap.set(word, freqMap.get(word) + 1 || 1);
  }

  // sorting the words based on frequency and lexicographical order
  const sortedWords = Array.from(freqMap.keys()).sort((a, b) => {
    const freqA = freqMap.get(a);
    const freqB = freqMap.get(b);

    if (freqA === freqB) {
      return a.localeCompare(b);
    } else {
      return freqB - freqA;
    }
  });
  // returning the top k frequent words
  return sortedWords.slice(0, k);
}

// Example:
console.log(topKFrequent(["i", "love", "leetcode", "i", "love", "coding"], 2));
// Output: ["i", "love"]

console.log(
  topKFrequent(
    ["the", "day", "is", "sunny", "the", "the", "the", "sunny", "is", "is"],
    4
  )
);
// Output: ["the", "is", "sunny", "day"]
```

<hr/>

💡 **Question-7:** **Sliding Window Maximum**

You are given an array of integers `nums`, there is a sliding window of size `k` which is moving from the very left of the array to the very right. You can only see the `k` numbers in the window. Each time the sliding window moves right by one position.

Return *the max sliding window*.

Example 1:

```
Input: nums = [1,3,-1,-3,5,3,6,7], k = 3
Output: [3,3,5,5,6,7]
Explanation:
Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6 7         3
 1 [3  -1  -3] 5  3  6 7         3
 1  3 [-1  -3  5] 3  6 7         5
 1  3  -1 [-3  5  3] 6 7         5
 1  3  -1  -3 [5  3  6]7         6
 1  3  -1  -3  5 [3  6  7]       7
```

Example 2:

```
Input: nums = [1], k = 1
Output: [1]
```

Constraints:

- `1 <= nums.length <= 100000`
- -`10000 <= nums[i] <= 10000`
- `1 <= k <= nums.length`

💬 **Solution-7:**

```js
function maxSlidingWindow(nums, k) {
  const result = [];
  const deque = [];

  for (let i = 0; i < nums.length; i++) {
    while (deque.length && deque[0] <= i - k) {
      deque.shift();
    }

    while (deque.length && nums[deque[deque.length - 1]] < nums[i]) {
      deque.pop();
    }
    deque.push(i);

    if (i >= k - 1) {
      result.push(nums[deque[0]]);
    }
  }
  return result;
}

// Example:
console.log(maxSlidingWindow([1, 3, -1, -3, 5, 3, 6, 7], 3));
// Output: [3, 3, 5, 5, 6, 7]
```

<hr/>

💡 **Question-8:** **Find K Closest Elements**

Given a **sorted** integer array `arr`, two integers `k` and `x`, return the `k` closest integers to `x` in the array. The result should also be sorted in ascending order.

An integer `a` is closer to `x` than an integer `b` if:

- `|a - x| < |b - x|`, or
- `|a - x| == |b - x|` and `a < b`

Example 1:

```
Input: arr = [1,2,3,4,5], k = 4, x = 3
Output: [1,2,3,4]
```

Example 2:

```
Input: arr = [1,2,3,4,5], k = 4, x = -1
Output: [1,2,3,4]
```

Constraints:

- `1 <= k <= arr.length`
- `1 <= arr.length <= 10000`
- `arr` is sorted in **ascending** order.
- -`10000 <= arr[i], x <= 10000`

💬 **Solution-8:**

```js
function findClosestElements(arr, k, x) {
  let left = 0;
  let right = arr.length - k;

  while (left < right) {
    const mid = Math.floor((left + right) / 2);
    if (x - arr[mid] > arr[mid + k] - x) {
      left = mid + 1;
    } else {
      right = mid;
    }
  }
  return arr.slice(left, left + k);
}

// Example:
console.log(findClosestElements([1, 2, 3, 4, 5], 4, 3));
// Output: [1, 2, 3, 4]

console.log(findClosestElements([1, 2, 3, 4, 5], 4, -1));
// Output: [1, 2, 3, 4]
```

<hr/>