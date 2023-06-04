# Assignment-9 Questions & Solutions

💡 **Question-1:** Given an integer `n`, return `true` if it is a power of two. Otherwise, return `false`.

An integer `n` is a power of two, if there exists an integer `x` such that `n == 2x`.

Example 1: Input: n = 1 Output: true

Example 2: Input: n = 3 Output: false

💬 **Solution-1:**

```js
function isPowerOfTwo(n) {
  if (n <= 0) {
    return false;
  }
  return (n & (n - 1)) === 0;
}

// Example:
console.log(isPowerOfTwo(1)); // Output: true
console.log(isPowerOfTwo(16)); // Output: true
console.log(isPowerOfTwo(3)); // Output: false
```

<hr/>

💡 **Question-2:** Given a number n, find the sum of the first natural numbers.

Example 1: Input: n = 3 Output: 6

Example 2: Input  : 5 Output : 15

💬 **Solution-2:**

```js
function sumOfFirstNNumbers(n) {
  return (n * (n + 1)) / 2;
}

// Example:
console.log(sumOfFirstNNumbers(3)); // Output: 6
console.log(sumOfFirstNNumbers(5)); // Output: 15
```

<hr/>

💡 **Question-3:** Given a positive integer, N. Find the factorial of N. 

Example 1: Input: N = 5 Output: 120

Example 2: Input: N = 4 Output: 24

💬 **Solution-3:**

```js
function factorial(N) {
  let result = 1;

  for (let i = 1; i <= N; i++) {
    result *= i;
  }
  return result;
}

// Example:
console.log(factorial(5)); // Output: 120
console.log(factorial(4)); // Output: 24
```

<hr/>

💡 **Question-4:** Given a number N and a power P, the task is to find the exponent of this number raised to the given power, i.e. N^P.

Example 1: Input: N = 5, P = 2 Output: 25

Example 2 : Input: N = 2, P = 5 Output: 32

💬 **Solution-4:**

```js
function calculateExponent(N, P) {
  return Math.pow(N, P);
}

// Example:
console.log(calculateExponent(5, 2)); // Output: 25
console.log(calculateExponent(2, 5)); // Output: 32
```

<hr/>

💡 **Question-5:** Given an array of integers arr, the task is to find maximum element of that array using recursion.

Example 1: Input: arr = {1, 4, 3, -5, -4, 8, 6}; Output: 8

Example 2: Input: arr = {1, 4, 45, 6, 10, -8}; Output: 45

💬 **Solution-5:**

```js
function findMax(arr, index) {
  if (index === arr.length) {
    return -Infinity;
  }

  const currentElement = arr[index];
  const maxSoFar = findMax(arr, index + 1);
  return Math.max(currentElement, maxSoFar);
}

function findMaximum(arr) {
  return findMax(arr, 0);
}

// Example:
console.log(findMaximum([1, 4, 3, -5, -4, 8, 6])); // Output: 8
console.log(findMaximum([1, 4, 45, 6, 10, -8])); // Output: 45
```

<hr/>

💡 **Question-6:** Given first term (a), common difference (d) and a integer N of the Arithmetic Progression series, the task is to find Nth term of the series.

Example 1: Input : a = 2 d = 1 N = 5 Output : 6
The 5th term of the series is : 6

Example 2: Input : a = 5 d = 2 N = 10 Output : 23
The 10th term of the series is : 23

💬 **Solution-6:**

```js
function findNthTerm(a, d, N) {
  return a + (N - 1) * d;
}

// Example:
console.log(findNthTerm(2, 1, 5)); // Output: 6
console.log(findNthTerm(5, 2, 10)); // Output: 23
```

<hr/>

💡 **Question-7:** Given a string S, the task is to write a program to print all permutations of a given string.

Example 1: Input: S = “ABC” Output: “ABC”, “ACB”, “BAC”, “BCA”, “CBA”, “CAB”

Example 2: Input: S = “XY” Output: “XY”, “YX”

💬 **Solution-7:**

```js
function permuteString(str) {
  const chars = str.split('');
  const result = [];

  function permuteHelper(startIndex) {
    if (startIndex === chars.length - 1) {
      result.push(chars.join(''));
      return;
    }

    for (let i = startIndex; i < chars.length; i++) {
      [chars[startIndex], chars[i]] = [chars[i], chars[startIndex]];

      permuteHelper(startIndex + 1);
      [chars[startIndex], chars[i]] = [chars[i], chars[startIndex]];
    }
  }
  permuteHelper(0);
  return result;
}

// Example:
console.log(permuteString('ABC')); // Output: ["ABC", "ACB", "BAC", "BCA", "CBA", "CAB"]
console.log(permuteString('XY')); // Output: ["XY", "YX"]
```

<hr/>

💡 **Question-8:** Given an array, find a product of all array elements.

Example 1: Input  : arr[] = {1, 2, 3, 4, 5} Output : 120

Example 2: Input  : arr[] = {1, 6, 3} Output : 18

💬 **Solution-8:**

```js
function productOfArrayElements(arr) {
  let product = 1;

  for (let i = 0; i < arr.length; i++) {
    product *= arr[i];
  }
  return product;
}

// Example:
console.log(productOfArrayElements([1, 2, 3, 4, 5])); // Output: 120
console.log(productOfArrayElements([1, 6, 3])); // Output: 18
```

<hr/>