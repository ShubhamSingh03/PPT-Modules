# Assignment-7 Questions & Solutions

💡 **Question-1:** Given two strings s and t, determine if they are isomorphic.

Two strings s and t are isomorphic if the characters in s can be replaced to get t.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character, but a character may map to itself.

Example: Input: s = "egg", t = "add" Output: true

💬 **Solution-1:**

```js
function isIsomorphic(s, t) {
  if (s.length !== t.length) {
    return false;
  }
  
  const sMap = new Map();
  const tMap = new Map();
  
  for (let i = 0; i < s.length; i++) {
    const sChar = s[i];
    const tChar = t[i];
    
    if (!sMap.has(sChar) && !tMap.has(tChar)) {
      sMap.set(sChar, tChar);
      tMap.set(tChar, sChar);
    }
    else if (sMap.get(sChar) !== tChar || tMap.get(tChar) !== sChar) {
      return false;
    }
  }
  return true;
}

// Example:
const s = "egg";
const t = "add";
console.log(isIsomorphic(s, t)); // Output: true
```

<hr/>

💡 **Question-2:** Given a string num which represents an integer, return true if num is a strobogrammatic number.

A strobogrammatic number is a number that looks the same when rotated 180 degrees (looked at upside down).

Example: Input: num = "69" Output: true

💬 **Solution-2:**

```js
function isStrobogrammatic(num) {
  const map = {
    '0': '0',
    '1': '1',
    '6': '9',
    '8': '8',
    '9': '6'
  };

  let rotatedNum = '';

  for (let i = num.length - 1; i >= 0; i--) {
    const digit = num[i];
    if (!map.hasOwnProperty(digit)) {
      return false;
    }
    rotatedNum += map[digit];
  }
  return rotatedNum === num;
}

// Example:
const num = "69";
console.log(isStrobogrammatic(num)); // Output: true
```

<hr/>

💡 **Question-3:** Given two non-negative integers, num1 and num2 represented as string, return the sum of num1 and num2 *as a string.

You must solve the problem without using any built-in library for handling large integers (such as BigInteger). You must also not convert the inputs to integers directly.

Example: Input: num1 = "11", num2 = "123" Output: "134"

💬 **Solution-3:**

```js
function addStrings(num1, num2) {
  let sum = '';
  let carry = 0;
  let i = num1.length - 1;
  let j = num2.length - 1;

  while (i >= 0 || j >= 0 || carry > 0) {
    const digit1 = i >= 0 ? parseInt(num1[i]) : 0;
    const digit2 = j >= 0 ? parseInt(num2[j]) : 0;

    const currentSum = digit1 + digit2 + carry;
    const currentDigit = currentSum % 10;
    carry = Math.floor(currentSum / 10);

    sum = currentDigit.toString() + sum;

    i--;
    j--;
  }
  return sum;
}

// Example:
const num1 = "11";
const num2 = "123";
console.log(addStrings(num1, num2)); // Output: "134"
```

<hr/>

💡 **Question-4:** Given a string s, reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.

Example: Input: s = "Let's take LeetCode contest" Output: "s'teL ekat edoCteeL tsetnoc"

💬 **Solution-4:**

```js
function reverseWords(s) {
  const words = s.split(' ');

  for (let i = 0; i < words.length; i++) {
    words[i] = reverseString(words[i]);
  }
  return words.join(' ');
}

function reverseString(str) {
  let reversed = '';
  for (let i = str.length - 1; i >= 0; i--) {
    reversed += str[i];
  }
  return reversed;
}

// Example:
const s = "Let's take LeetCode contest";
console.log(reverseWords(s)); // Output: "s'teL ekat edoCteeL tsetnoc"
```

<hr/>

💡 **Question-5:** Given a string s and an integer k, reverse the first k characters for every 2k characters counting from the start of the string.

If there are fewer than k characters left, reverse all of them. If there are less than 2k but greater than or equal to k characters, then reverse the first k characters and leave the other as original.

Example: Input: s = "abcdefg", k = 2 Output: "bacdfeg"

💬 **Solution-5:**

```js
function reverseStr(s, k) {
  const arr = s.split('');

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
  return arr.join('');
}

// Example:
const s = "abcdefg";
const k = 2;
console.log(reverseStr(s, k)); // Output: "bacdfeg"
```

<hr/>

💡 **Question-6:** Given two strings s and goal, return true if and only if s can become goal after some number of shifts on s.

A shift on s consists of moving the leftmost character of s to the rightmost position.

- For example, if s = "abcde", then it will be "bcdea" after one shift.

Example: Input: s = "abcde", goal = "cdeab" Output: true

💬 **Solution-6:**

```js
function rotateString(s, goal) {
  if (s.length !== goal.length) {
    return false;
  }

  const concatenated = s + s;
  return concatenated.includes(goal);
}

// Example:
const s = "abcde";
const goal = "cdeab";
console.log(rotateString(s, goal)); // Output: true
```

<hr/>

💡 **Question-7:** Given two strings s and t, return true if they are equal when both are typed into empty text editors. '#' means a backspace character.

Note that after backspacing an empty text, the text will continue empty.

Example: Input: s = "ab#c", t = "ad#c" Output: true

💬 **Solution-7:**

```js
function backspaceCompare(s, t) {
  const stackS = buildStack(s);
  const stackT = buildStack(t);

  if (stackS.length !== stackT.length) {
    return false;
  }
  while (stackS.length > 0) {
    if (stackS.pop() !== stackT.pop()) {
      return false;
    }
  }
  return true;
}

function buildStack(str) {
  const stack = [];
  for (let i = 0; i < str.length; i++) {
    if (str[i] !== '#') {
      stack.push(str[i]);
    } else {
      stack.pop();
    }
  }
  return stack;
}

// Example:
const s = "ab#c";
const t = "ad#c";
console.log(backspaceCompare(s, t)); // Output: true
```

<hr/>

💡 **Question-8:** You are given an array coordinates, coordinates[i] = [x, y], where [x, y] represents the coordinate of a point. Check if these points make a straight line in the XY plane.

![assignment-7-strings-question-8-image](./images/assignment-7-strings-question-8.png)

Example: Input: coordinates = [[1,2],[2,3],[3,4],[4,5],[5,6],[6,7]] Output: true

💬 **Solution-8:**

```js
function checkStraightLine(coordinates) {
  if (coordinates.length <= 2) {
    return true;
  }

  const [x0, y0] = coordinates[0];
  const [x1, y1] = coordinates[1];
  const initialSlope = calculateSlope(x0, y0, x1, y1);

  for (let i = 2; i < coordinates.length; i++) {
    const [x, y] = coordinates[i];
    const slope = calculateSlope(x0, y0, x, y);
    if (slope !== initialSlope) {
      return false; // Slopes are different, not a straight line
    }
  }
  return true; // All slopes are the same, forms a straight line
}

function calculateSlope(x1, y1, x2, y2) {
  return (y2 - y1) / (x2 - x1);
}

// Example:
const coordinates = [[1, 2], [2, 3], [3, 4], [4, 5], [5, 6], [6, 7]];
console.log(checkStraightLine(coordinates)); // Output: true
```

<hr/>