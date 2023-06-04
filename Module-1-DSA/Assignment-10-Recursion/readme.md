# Assignment-10 Questions & Solutions

💡 **Question-1:** Given an integer `n`, return `true` if it is a power of three. Otherwise, return `false`.

An integer `n` is a power of three, if there exists an integer `x` such that `n == 3x`.

Example 1:

```
Input: n = 27
Output: true
Explanation: 27 = 33
```

Example 2:

```
Input: n = 0
Output: false
Explanation: There is no x where 3x = 0.
```

💬 **Solution-1:**

```js
function isPowerOfThree(n) {
  if (n <= 0) {
    return false; 
  }
  const logarithm = Math.log10(n) / Math.log10(3);
  return Number.isInteger(logarithm);
}

// Example:
console.log(isPowerOfThree(27)); // Output: true
console.log(isPowerOfThree(0)); // Output: false
```

<hr/>

💡 **Question-2:** You have a list `arr` of all integers in the range `[1, n]` sorted in a strictly increasing order. Apply the following algorithm on `arr`:

- Starting from left to right, remove the first number and every other number afterward until you reach the end of the list.
- Repeat the previous step again, but this time from right to left, remove the rightmost number and every other number from the remaining numbers.
- Keep repeating the steps again, alternating left to right and right to left, until a single number remains.

Given the integer `n`, return the last number that remains in `arr`.

Example 1:

```
Input: n = 9
Output: 6
Explanation:
arr = [1, 2,3, 4,5, 6,7, 8,9]
arr = [2,4, 6,8]
arr = [2, 6]
arr = [6]
```

Example 2:
```
Input: n = 1
Output: 1
```

💬 **Solution-2:**

```js
function lastRemaining(n) {
  let arr = Array.from({ length: n }, (_, i) => i + 1);
  let leftToRight = true;

  while (arr.length > 1) {
    if (leftToRight) {
      arr = arr.filter((_, index) => (index + 1) % 2 === 0);
    } else {
      arr = arr.filter((_, index) => index % 2 === 0);
    }
    leftToRight = !leftToRight;
  }
  return arr[0];
}

// Example:
console.log(lastRemaining(9)); // Output: 6
console.log(lastRemaining(1)); // Output: 1
```

<hr/>

💡 **Question-3:** Given a set represented as a string, write a recursive code to print all subsets of it. The subsets can be printed in any order.

Example 1: Input :  set = “abc” Output : { “”, “a”, “b”, “c”, “ab”, “ac”, “bc”, “abc”}

Example 2: Input : set = “abcd” Output : { “”, “a” ,”ab” ,”abc” ,”abcd”, “abd” ,”ac” ,”acd”, “ad” ,”b”, “bc” ,”bcd” ,”bd” ,”c” ,”cd” ,”d” }

💬 **Solution-3:**

```js
function subsets(setStr) {
  const result = [];
  generateSubsets(setStr, '', 0, result);
  return result;
}

function generateSubsets(setStr, currentSet, index, result) {
  if (index === setStr.length) {
    result.push(currentSet);
    return;
  }

  generateSubsets(setStr, currentSet + setStr[index], index + 1, result);
  generateSubsets(setStr, currentSet, index + 1, result);
}

// Example:
console.log(subsets('abc')); // Output: ["", "a", "ab", "abc", "ac", "b", "bc", "c"]
console.log(subsets('abcd')); // Output: ["", "a", "ab", "abc", "abcd", "abd", "ac", "acd", "ad", "b", "bc", "bcd", "bd", "c", "cd", "d"]
```

<hr/>

💡 **Question-4:** Given a string calculate length of the string using recursion.

Examples:

```
Input : str = "abcd"
Output :4

Input : str = "GEEKSFORGEEKS"
Output :13
```

💬 **Solution-4:**

```js
function stringLength(str) {
  if (str === '') {
    return 0;
  }
  return 1 + stringLength(str.slice(1));
}

// Example:
console.log(stringLength('abcd')); // Output: 4
console.log(stringLength('GEEKSFORGEEKS')); // Output: 13
```

<hr/>

💡 **Question-5:** We are given a string S, we need to find count of all contiguous substrings starting and ending with same character.

Examples :

```
Input  : S = "abcab"
Output : 7
There are 15 substrings of "abcab"
a, ab, abc, abca, abcab, b, bc, bca
bcab, c, ca, cab, a, ab, b
Out of the above substrings, there
are 7 substrings : a, abca, b, bcab,
c, a and b.

Input  : S = "aba"
Output : 4
The substrings are a, b, a and aba
```

💬 **Solution-5:**

```js
function countSubstrings(S) {
  let count = 0;

  for (let i = 0; i < S.length; i++) {
    count++; 
    for (let j = i + 1; j < S.length; j++) {
      if (S[i] === S[j]) {
        count++;
      }
    }
  }
  return count;
}

// Example:
console.log(countSubstrings('abcab')); // Output: 7
console.log(countSubstrings('aba')); // Output: 4
```

<hr/>

💡 **Question-6:** The tower of Hanoi is a famous puzzle where we have three rods and N disks. The objective of the puzzle is to move the entire stack to another rod. You are given the number of discs N. Initially, these discs are in the rod 1. You need to print all the steps of discs movement so that all the discs reach the 3rd rod. Also, you need to find the total moves.Note: The discs are arranged such that the top disc is numbered 1 and the bottom-most disc is numbered N. Also, all the discs have different sizes and a bigger disc cannot be put on the top of a smaller disc. Refer the provided link to get a better clarity about the puzzle.

Example 1:
```
Input:
N = 2
Output:
move disk 1 from rod 1 to rod 2
move disk 2 from rod 1 to rod 3
move disk 1 from rod 2 to rod 3
3
Explanation:For N=2 , steps will be
as follows in the example and total
3 steps will be taken.
```

Example 2:
```
Input:
N = 3
Output:
move disk 1 from rod 1 to rod 3
move disk 2 from rod 1 to rod 2
move disk 1 from rod 3 to rod 2
move disk 3 from rod 1 to rod 3
move disk 1 from rod 2 to rod 1
move disk 2 from rod 2 to rod 3
move disk 1 from rod 1 to rod 3
7
Explanation:For N=3 , steps will be
as follows in the example and total
7 steps will be taken.
```

💬 **Solution-6:**

```js
function towerOfHanoi(N, source, destination, auxiliary) {
  if (N === 1) {
    console.log(`Move disk 1 from rod ${source} to rod ${destination}`);
    return 1;
  }

  let moves = 0;
  moves += towerOfHanoi(N - 1, source, auxiliary, destination);

  console.log(`Move disk ${N} from rod ${source} to rod ${destination}`);

  moves++;
  moves += towerOfHanoi(N - 1, auxiliary, destination, source);
  return moves;
}

// Example:
console.log(towerOfHanoi(2, 1, 3, 2)); // Output: 3
console.log(towerOfHanoi(3, 1, 3, 2)); // Output: 7
```

<hr/>

💡 **Question-7:** Given a string str, the task is to print all the permutations of str. A permutation is an arrangement of all or part of a set of objects, with regard to the order of the arrangement. For instance, the words ‘bat’ and ‘tab’ represents two distinct permutation (or arrangements) of a similar three letter word.

Examples:
Input: str = “cd” Output: cd dc

Input: str = “abb” Output: abb abb bab bba bab bba

💬 **Solution-7:**

```js
function permutations(str) {
  const result = [];
  generatePermutations(str, '', result);
  return result;
}

function generatePermutations(remaining, current, result) {
  if (remaining === '') {
    result.push(current);
    return;
  }

  for (let i = 0; i < remaining.length; i++) {
    const newRemaining = remaining.slice(0, i) + remaining.slice(i + 1); 
    generatePermutations(newRemaining, current + remaining[i], result); 
  }
}

// Examples:
console.log(permutations('cd')); // Output: ["cd", "dc"]
console.log(permutations('abb')); // Output: ["abb", "bab", "bba", "abb", "bab", "bba"]
```

<hr/>

💡 **Question-8:** Given a string, count total number of consonants in it. A consonant is an English alphabet character that is not vowel (a, e, i, o and u). Examples of constants are b, c, d, f, and g.

Examples:
```
Input : abc de
Output : 3
There are three consonants b, c and d.

Input : geeksforgeeks portal
Output : 12
```

💬 **Solution-8:**

```js
function countConsonants(str) {
  const consonants = 'bcdfghjklmnpqrstvwxyz';
  let count = 0;

  for (let i = 0; i < str.length; i++) {
    const char = str[i].toLowerCase();
    if (consonants.includes(char)) {
      count++;
    }
  }
  return count;
}

// Examples:
console.log(countConsonants('abc de')); // Output: 3
console.log(countConsonants('geeksforgeeks portal')); // Output: 12
```

<hr/>