# Assignment-16 Questions & Solutions

💡 **Question-1:** Given an array, for each element find the value of the nearest element to the right which is having a frequency greater than that of the current element. If there does not exist an answer for a position, then make the value ‘-1’.

Examples:

```
Input: a[] = [1, 1, 2, 3, 4, 2, 1]
Output : [-1, -1, 1, 2, 2, 1, -1]

Explanation:
Given array a[] = [1, 1, 2, 3, 4, 2, 1]
Frequency of each element is: 3, 3, 2, 1, 1, 2, 3

Lets calls Next Greater Frequency element as NGF
1. For element a[0] = 1 which has a frequency = 3,
   As it has frequency of 3 and no other next element
   has frequency more than 3 so  '-1'
2. For element a[1] = 1 it will be -1 same logic
   like a[0]
3. For element a[2] = 2 which has frequency = 2,
   NGF element is 1 at position = 6  with frequency
   of 3 > 2
4. For element a[3] = 3 which has frequency = 1,
   NGF element is 2 at position = 5 with frequency
   of 2 > 1
5. For element a[4] = 4 which has frequency = 1,
   NGF element is 2 at position = 5 with frequency
   of 2 > 1
6. For element a[5] = 2 which has frequency = 2,
   NGF element is 1 at position = 6 with frequency
   of 3 > 2
7. For element a[6] = 1 there is no element to its
   right, hence -1
```

```
Input : a[] = [1, 1, 1, 2, 2, 2, 2, 11, 3, 3]
Output : [2, 2, 2, -1, -1, -1, -1, 3, -1, -1]
```

💬 **Solution-1:**

```js
function findNearestGreaterFrequency(arr) {
  const frequencyMap = {};
  const result = [];

  // counting the frequency of each element
  for (let i = arr.length - 1; i >= 0; i--) {
    if (!frequencyMap.hasOwnProperty(arr[i])) {
      frequencyMap[arr[i]] = 1;
    } else {
      frequencyMap[arr[i]]++;
    }
  }

  // finding the nearest greater frequency element
  for (let i = 0; i < arr.length; i++) {
    let nextGreaterFrequency = -1;
    for (let j = i + 1; j < arr.length; j++) {
      if (frequencyMap[arr[j]] > frequencyMap[arr[i]]) {
        nextGreaterFrequency = arr[j];
        break;
      }
    }
    result.push(nextGreaterFrequency);
  }
  return result;
}

// Example:
const arr1 = [1, 1, 2, 3, 4, 2, 1];
const result1 = findNearestGreaterFrequency(arr1);
console.log(result1); // Output: [-1, -1, 1, 2, 2, 1, -1]

const arr2 = [1, 1, 1, 2, 2, 2, 2, 11, 3, 3];
const result2 = findNearestGreaterFrequency(arr2);
console.log(result2); // Output: [2, 2, 2, -1, -1, -1, -1, 3, -1, -1]
```

<hr/>

💡 **Question-2:** Given a stack of integers, sort it in ascending order using another temporary stack.

Examples:

```
Input : [34, 3, 31, 98, 92, 23]
Output : [3, 23, 31, 34, 92, 98]

Input : [3, 5, 1, 4, 2, 8]
Output : [1, 2, 3, 4, 5, 8]
```

💬 **Solution-2:**

```js
function sortStack(stack) {
  const tempStack = [];

  while (stack.length > 0) {
    const temp = stack.pop();

    while (tempStack.length > 0 && tempStack[tempStack.length - 1] > temp) {
      stack.push(tempStack.pop());
    }
    tempStack.push(temp);
  }
  return tempStack;
}

// Example:
const stack1 = [34, 3, 31, 98, 92, 23];
const sortedStack1 = sortStack(stack1);
console.log(sortedStack1); // Output: [3, 23, 31, 34, 92, 98]

const stack2 = [3, 5, 1, 4, 2, 8];
const sortedStack2 = sortStack(stack2);
console.log(sortedStack2); // Output: [1, 2, 3, 4, 5, 8]
```

<hr/>

💡 **Question-3:** Given a stack with **push()**, **pop()**, and **empty()** operations, The task is to delete the **middle** element of it without using any additional data structure.

```
Input  : Stack[] = [1, 2, 3, 4, 5]
Output : Stack[] = [1, 2, 4, 5]

Input  : Stack[] = [1, 2, 3, 4, 5, 6]
Output : Stack[] = [1, 2, 4, 5, 6]
```

💬 **Solution-3:**

```js
function deleteMiddle(stack) {
  if (stack.length === 0 || stack.length === 1) {
    return stack;
  }

  const temp = stack.pop();
  deleteMiddle(stack);

  const stackSize = stack.length;
  if (stackSize % 2 === 1) {
    stack.push(temp);
  }
  return stack;
}

// Example:
const stack1 = [1, 2, 3, 4, 5];
const modifiedStack1 = deleteMiddle(stack1);
console.log(modifiedStack1); // Output: [1, 2, 4, 5]

const stack2 = [1, 2, 3, 4, 5, 6];
const modifiedStack2 = deleteMiddle(stack2);
console.log(modifiedStack2); // Output: [1, 2, 4, 5, 6]
```

<hr/>

💡 **Question-4:** Given a Queue consisting of first **n** natural numbers (in random order). The task is to check whether the given Queue elements can be arranged in increasing order in another Queue using a stack. The operation allowed are:

1. Push and pop elements from the stack
2. Pop (Or Dequeue) from the given Queue.
3. Push (Or Enqueue) in the another Queue.

Examples:

```
Input : Queue[] = { 5, 1, 2, 3, 4 } 
Output : Yes 
Pop the first element of the given Queue 
i.e 5. Push 5 into the stack. 
Now, pop all the elements of the given Queue and push them to second Queue. 
Now, pop element 5 in the stack and push it to the second Queue.   

Input : Queue[] = { 5, 1, 2, 6, 3, 4 } 
Output : No 
Push 5 to stack. 
Pop 1, 2 from given Queue and push it to another Queue. 
Pop 6 from given Queue and push to stack. 
Pop 3, 4 from given Queue and push to second Queue. 
Now, from using any of above operation, we cannot push 5 into the second Queue because it is below the 6 in the stack.
```

💬 **Solution-4:**

```js
function canArrangeInIncreasingOrder(queue) {
  const stack = [];
  const secondQueue = [];

  while (queue.length > 0) {
    const currentElement = queue.shift();

    while (stack.length > 0 && stack[stack.length - 1] < currentElement) {
      secondQueue.push(stack.pop());
    }
    stack.push(currentElement);
  }

  while (stack.length > 0) {
    secondQueue.push(stack.pop());
  }

  let sorted = true;
  for (let i = 1; i < secondQueue.length; i++) {
    if (secondQueue[i] < secondQueue[i - 1]) {
      sorted = false;
      break;
    }
  }

  if (queue.length === 0 && sorted) {
    return "Yes";
  } else {
    return "No";
  }
}

// Example:
const queue1 = [5, 1, 2, 3, 4];
const result1 = canArrangeInIncreasingOrder(queue1);
console.log(result1); // Output: Yes

const queue2 = [5, 1, 2, 6, 3, 4];
const result2 = canArrangeInIncreasingOrder(queue2);
console.log(result2); // Output: No
```

<hr/>

💡 **Question-5:** Given a number , write a program to reverse this number using stack.

Examples:

```
Input : 365
Output : 563

Input : 6899
Output : 9986
```

💬 **Solution-5:**

```js
function reverseNumber(number) {
  const numberString = number.toString();
  const stack = [];

  for (let i = 0; i < numberString.length; i++) {
    stack.push(numberString.charAt(i));
  }

  let reversedNumber = "";
  while (stack.length > 0) {
    reversedNumber += stack.pop();
  }
  return parseInt(reversedNumber, 10);
}

// Example:
const number1 = 365;
const reversedNumber1 = reverseNumber(number1);
console.log(reversedNumber1); // Output: 563

const number2 = 6899;
const reversedNumber2 = reverseNumber(number2);
console.log(reversedNumber2); // Output: 9986
```

<hr/>

💡 **Question-6:** Given an integer k and a **[queue](https://www.geeksforgeeks.org/queue-data-structure/)** of integers, The task is to reverse the order of the first **k** elements of the queue, leaving the other elements in the same relative order.

Only following standard operations are allowed on queue.

- **enqueue(x) :** Add an item x to rear of queue
- **dequeue() :** Remove an item from front of queue
- **size() :** Returns number of elements in queue.
- **front() :** Finds front item.

💬 **Solution-6:**

```js
function reverseKElements(queue, k) {
  if (k <= 0 || k > queue.length) {
    return "Invalid value of k.";
  }

  const stack = [];

  // dequeuing the first k elements and push them onto the stack
  for (let i = 0; i < k; i++) {
    stack.push(queue.shift());
  }

  // dequeuing remaining elements and enqueue them back into the queue
  while (queue.length > 0) {
    queue.push(queue.shift());
  }

  // dequeuing elements from the stack and enqueue them back into the queue
  while (stack.length > 0) {
    queue.push(stack.pop());
  }
  return queue;
}

// Example:
const queue1 = [1, 2, 3, 4, 5];
const k1 = 3;
const reversedQueue1 = reverseKElements(queue1, k1);
console.log(reversedQueue1); // Output: [3, 2, 1, 4, 5]

const queue2 = [10, 20, 30, 40, 50, 60];
const k2 = 5;
const reversedQueue2 = reverseKElements(queue2, k2);
console.log(reversedQueue2); // Output: [50, 40, 30, 20, 10, 60]
```

<hr/>

💡 **Question-7:** Given a sequence of n strings, the task is to check if any two similar words come together and then destroy each other then print the number of words left in the sequence after this pairwise destruction.

Examples:

```
Input : ab aa aa bcd ab
Output : 3
Explanation: As aa, aa destroys each other so,
ab bcd ab is the new sequence.

Input :  tom jerry jerry tom
Output : 0
Explanation: As first both jerry will destroy each other.
Then sequence will be tom, tom they will also destroy
each other. So, the final sequence doesn’t contain any
word.
```

💬 **Solution-7:**

```js
function countWordsLeft(sequence) {
  const words = sequence.split(" ");
  const stack = [];

  for (let i = 0; i < words.length; i++) {
    const currentWord = words[i];

    if (stack.length > 0 && currentWord === stack[stack.length - 1]) {
      stack.pop();
    } else {
      stack.push(currentWord);
    }
  }
  return stack.length;
}

// Example:
const sequence1 = "ab aa aa bcd ab";
const result1 = countWordsLeft(sequence1);
console.log(result1); // Output: 3

const sequence2 = "tom jerry jerry tom";
const result2 = countWordsLeft(sequence2);
console.log(result2); // Output: 0
```

<hr/>

💡 **Question-8:** Given an array of integers, the task is to find the maximum absolute difference between the nearest left and the right smaller element of every element in the array.

**Note:** If there is no smaller element on right side or left side of any element then we take zero as the smaller element. For example for the leftmost element, the nearest smaller element on the left side is considered as 0. Similarly, for rightmost elements, the smaller element on the right side is considered as 0.

Examples:

```
Input : arr[] = {2, 1, 8}
Output : 1
Left smaller  LS[] {0, 0, 1}
Right smaller RS[] {1, 0, 0}
Maximum Diff of abs(LS[i] - RS[i]) = 1

Input  : arr[] = {2, 4, 8, 7, 7, 9, 3}
Output : 4
Left smaller   LS[] = {0, 2, 4, 4, 4, 7, 2}
Right smaller  RS[] = {0, 3, 7, 3, 3, 3, 0}
Maximum Diff of abs(LS[i] - RS[i]) = 7 - 3 = 4

Input : arr[] = {5, 1, 9, 2, 5, 1, 7}
Output : 1
```

💬 **Solution-8:**

```js
function maxDiffNearestSmaller(arr) {
  const n = arr.length;
  const leftSmaller = new Array(n).fill(0);
  const rightSmaller = new Array(n).fill(0);
  const stack = [];

  // calculating the nearest smaller element on the right
  for (let i = 0; i < n; i++) {
    while (stack.length > 0 && arr[i] < arr[stack[stack.length - 1]]) {
      const poppedIndex = stack.pop();
      rightSmaller[poppedIndex] = arr[i];
    }
    stack.push(i);
  }

  // clearing the stack
  while (stack.length > 0) {
    stack.pop();
  }

  // calculating the nearest smaller element on the left
  for (let i = n - 1; i >= 0; i--) {
    while (stack.length > 0 && arr[i] < arr[stack[stack.length - 1]]) {
      const poppedIndex = stack.pop();
      leftSmaller[poppedIndex] = arr[i];
    }
    stack.push(i);
  }

  let maxDiff = 0;

  // finding the maximum absolute difference
  for (let i = 0; i < n; i++) {
    const diff = Math.abs(leftSmaller[i] - rightSmaller[i]);
    if (diff > maxDiff) {
      maxDiff = diff;
    }
  }
  return maxDiff;
}

// Example:
const arr1 = [2, 1, 8];
const result1 = maxDiffNearestSmaller(arr1);
console.log(result1); // Output: 1

const arr2 = [2, 4, 8, 7, 7, 9, 3];
const result2 = maxDiffNearestSmaller(arr2);
console.log(result2); // Output: 4

const arr3 = [5, 1, 9, 2, 5, 1, 7];
const result3 = maxDiffNearestSmaller(arr3);
console.log(result3); // Output: 1
```

<hr/>