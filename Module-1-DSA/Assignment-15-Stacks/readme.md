# Assignment-15 Questions & Solutions

💡 **Question-1:** Given an array **arr[ ]** of size **N** having elements, the task is to find the next greater element for each element of the array in order of their appearance in the array.Next greater element of an element in the array is the nearest element on the right which is greater than the current element.If there does not exist next greater of current element, then next greater element for current element is -1. For example, next greater of the last element is always -1.

Example 1:

```
Input:
N = 4, arr[] = [1 3 2 4]
Output:
3 4 4 -1
Explanation:
In the array, the next larger element
to 1 is 3 , 3 is 4 , 2 is 4 and for 4 ?
since it doesn't exist, it is -1.
```

Example 2:

```
Input:
N = 5, arr[] [6 8 0 1 3]
Output:
8 -1 1 3 -1
Explanation:
In the array, the next larger element to
6 is 8, for 8 there is no larger elements
hence it is -1, for 0 it is 1 , for 1 it
is 3 and then for 3 there is no larger
element on right and hence -1.
```

💬 **Solution-1:**

```js
function nextGreaterElement(arr) {
  const result = [];
  const stack = [];
  
  for (let i = arr.length - 1; i >= 0; i--){
    while (stack.length > 0 && stack[stack.length - 1] <= arr[i]) {
      stack.pop();
    }
    
    if (stack.length === 0) {
      result.unshift(-1);
    } else {
      result.unshift(stack[stack.length - 1]);
    }
    stack.push(arr[i]);
  }
  return result;
}

// Example:
const arr1 = [1, 3, 2, 4];
console.log(nextGreaterElement(arr1)); // Output: [3, 4, 4, -1]

const arr2 = [6, 8, 0, 1, 3];
console.log(nextGreaterElement(arr2)); // Output: [8, -1, 1, 3, -1]
```

<hr/>

💡 **Question-2:** Given an array **a** of integers of length **n**, find the nearest smaller number for every element such that the smaller element is on left side.If no small element present on the left print -1.

Example 1:

```
Input: n = 3
a = {1, 6, 2}
Output: -1 1 1
Explaination: There is no number at the
left of 1. Smaller number than 6 and 2 is 1.
```

Example 2:

```
Input: n = 6
a = {1, 5, 0, 3, 4, 5}
Output: -1 1 -1 0 3 4
Explaination: Upto 3 it is easy to see
the smaller numbers. But for 4 the smaller
numbers are 1, 0 and 3. But among them 3
is closest. Similary for 5 it is 4.
```

💬 **Solution-2:**

```js
function nearestSmallerNumber(arr) {
  const result = [];
  const stack = [];

  for (let i = 0; i < arr.length; i++) {
    while (stack.length > 0 && stack[stack.length - 1] >= arr[i]) {
      stack.pop();
    }

    if (stack.length === 0) {
      result.push(-1);
    } else {
      result.push(stack[stack.length - 1]);
    }
    stack.push(arr[i]);
  }
  return result;
}

// Example:
const arr1 = [1, 6, 2];
console.log(nearestSmallerNumber(arr1)); // Output: [-1, 1, 1]

const arr2 = [1, 5, 0, 3, 4, 5];
console.log(nearestSmallerNumber(arr2)); // Output: [-1, 1, -1, 0, 3, 4]
```

<hr/>

💡 **Question-3:** Implement a Stack using two queues **q1** and **q2**.

Example 1:

```
Input:
push(2)
push(3)
pop()
push(4)
pop()
Output:3 4
Explanation:
push(2) the stack will be {2}
push(3) the stack will be {2 3}
pop()   poped element will be 3 the
        stack will be {2}
push(4) the stack will be {2 4}
pop()   poped element will be 4
```

Example 2:

```
Input:
push(2)
pop()
pop()
push(3)
Output:2 -1
```

💬 **Solution-3:**

```js
class Stack {
  constructor() {
    this.q1 = [];
    this.q2 = [];
  }

  push(element) {
    this.q1.push(element);
  }

  pop() {
    if (this.isEmpty()) {
      return -1;
    }
    while (this.q1.length > 1) {
      this.q2.push(this.q1.shift());
    }
    return this.q1.shift();
  }

  top() {
    if (this.isEmpty()) {
      return -1;
    }
    while (this.q1.length > 1) {
      this.q2.push(this.q1.shift());
    }

    const topElement = this.q1[0];
    this.q2.push(this.q1.shift());

    [this.q1, this.q2] = [this.q2, this.q1];
    return topElement;
  }
  isEmpty() {
    return this.q1.length === 0 && this.q2.length === 0;
  }
}

// Example:
const stack = new Stack();
stack.push(2);
stack.push(3);
console.log(stack.pop()); // Output: 3
stack.push(4);
console.log(stack.pop()); // Output: 4

const stack2 = new Stack();
stack2.push(2);
console.log(stack2.pop()); // Output: 2
console.log(stack2.pop()); // Output: -1
```

<hr/>

💡 **Question-4:** You are given a stack **St**. You have to reverse the stack using recursion.

Examples:

```
Input:St = {3,2,1,7,6}
Output:{6,7,1,2,3}

Input:St = {4,3,9,6}
Output:{6,9,3,4}
```

💬 **Solution-4:**

```js
function reverseStack(stack) {
  if (stack.length <= 1) {
    return stack;
  }

  const topElement = stack.pop();
  const reversedStack = reverseStack(stack);
  reversedStack.unshift(topElement);
  return reversedStack;
}

// Example:
const stack1 = [3, 2, 1, 7, 6];
console.log(reverseStack(stack1)); // Output: [6, 7, 1, 2, 3]

const stack2 = [4, 3, 9, 6];
console.log(reverseStack(stack2)); // Output: [6, 9, 3, 4]
```

<hr/>

💡 **Question-5:** You are given a string **S**, the task is to reverse the string using stack.

Example:

```
Input: S="GeeksforGeeks"
Output: skeeGrofskeeG
```

💬 **Solution-5:**

```js
function reverseString(str) {
  const stack = [];
  
  for (let i = 0; i < str.length; i++) {
    stack.push(str[i]);
  }
  
  let reversedStr = '';
  while (stack.length > 0) {
    reversedStr += stack.pop();
  }
  return reversedStr;
}

// Example:
const str = "GeeksforGeeks";
console.log(reverseString(str)); // Output: "skeeGrofskeeG"

```

<hr/>

💡 **Question-6:** Given string **S** representing a postfix expression, the task is to evaluate the expression and find the final value. Operators will only include the basic arithmetic operators like ***, /, + and -**.

Examples:

```
Input: S = "231*+9-"
Output: -4
Explanation:
After solving the given expression,
we have -4 as result.


Input: S = "123+*8-"
Output: -3
Explanation:
After solving the given postfix
expression, we have -3 as result.
```

💬 **Solution-6:**

```js
function evaluatePostfixExpression(expression) {
  const stack = [];

  for (let i = 0; i < expression.length; i++) {
    const char = expression[i];

    if (!isNaN(char)) {
      stack.push(parseInt(char));
    } else {
      const b = stack.pop();
      const a = stack.pop();

      let result;

      switch (char) {
        case '+':
          result = a + b;
          break;
        case '-':
          result = a - b;
          break;
        case '*':
          result = a * b;
          break;
        case '/':
          result = a / b;
          break;
      }
      stack.push(result);
    }
  }
  return stack[0];
}

// Example:
const expression1 = "231*+9-";
console.log(evaluatePostfixExpression(expression1)); // Output: -4

const expression2 = "123+*8-";
console.log(evaluatePostfixExpression(expression2)); // Output: -3
```

<hr/>

💡 **Question-7:** Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the `MinStack` class:

- `MinStack()` initializes the stack object.
- `void push(int val)` pushes the element `val` onto the stack.
- `void pop()` removes the element on the top of the stack.
- `int top()` gets the top element of the stack.
- `int getMin()` retrieves the minimum element in the stack.

You must implement a solution with `O(1)` time complexity for each function.

Example:

```
Input
["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]

Output
[null,null,null,null,-3,null,0,-2]

Explanation
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin(); // return -3
minStack.pop();
minStack.top();    // return 0
minStack.getMin(); // return -2
```

💬 **Solution-7:**

```js
class MinStack {
  constructor() {
    this.stack = [];
    this.minStack = []; // Stack to keep track of minimum elements
  }

  push(val) {
    this.stack.push(val);

    if (this.minStack.length === 0 || val <= this.minStack[this.minStack.length - 1]) {
      this.minStack.push(val);
    }
  }

  pop() {
    const val = this.stack.pop();

    if (val === this.minStack[this.minStack.length - 1]) {
      this.minStack.pop();
    }
  }

  top() {
    return this.stack[this.stack.length - 1];
  }

  getMin() {
    return this.minStack[this.minStack.length - 1];
  }
}

// Example:
const minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
console.log(minStack.getMin()); // Output: -3
minStack.pop();
console.log(minStack.top());    // Output: 0
console.log(minStack.getMin()); // Output: -2
```

<hr/>

💡 **Question-8:** Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

Examples:

```
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.


Input: height = [4,2,0,3,2,5]
Output: 9
```

💬 **Solution-8:**

```js
function trapWater(height) {
  let left = 0;
  let right = height.length - 1;
  let leftMax = 0;
  let rightMax = 0;
  let water = 0;

  while (left <= right) {
    if (height[left] <= height[right]) {
      leftMax = Math.max(leftMax, height[left]);
      water += leftMax - height[left];
      left++;
    } else {
      rightMax = Math.max(rightMax, height[right]);
      water += rightMax - height[right];
      right--;
    }
  }
  return water;
}

// Example:
const height1 = [0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1];
console.log(trapWater(height1)); // Output: 6

const height2 = [4, 2, 0, 3, 2, 5];
console.log(trapWater(height2)); // Output: 9
```

<hr/>