# Assignment-20 Questions & Solutions

💡 **Question-1:** Given a binary tree, your task is to find subtree with maximum sum in tree.

Examples:

Input1 :       

       1

     /   \

    2      3

    / \    / \

    4   5  6   7

Output1 : 28

As all the tree elements are positive, the largest subtree sum is equal to sum of all tree elements.

Input2 :

       1

     /    \

    -2      3

    / \    /  \

    4   5  -6   2

Output2 : 7

Subtree with largest sum is :

 -2

 / \

4   5

Also, entire tree sum is also 7.


💬 **Solution-1:**

```js
class Node {
  constructor(value) {
    this.value = value;
    this.left = null;
    this.right = null;
  }
}

function findMaxSubtreeSum(root) {
  let maxSum = -Infinity;

  function findMaxSum(node) {
    if (node === null) {
      return 0;
    }

    const leftSum = findMaxSum(node.left);
    const rightSum = findMaxSum(node.right);

    const subtreeSum = node.value + leftSum + rightSum;
    maxSum = Math.max(maxSum, subtreeSum);
    return subtreeSum;
  }

  findMaxSum(root);

  return maxSum;
}

// creating the binary tree for the first example
const root1 = new Node(1);
root1.left = new Node(2);
root1.right = new Node(3);
root1.left.left = new Node(4);
root1.left.right = new Node(5);
root1.right.left = new Node(6);
root1.right.right = new Node(7);

console.log(findMaxSubtreeSum(root1)); // Output: 28

// creating the binary tree for the second example
const root2 = new Node(1);
root2.left = new Node(-2);
root2.right = new Node(3);
root2.left.left = new Node(4);
root2.left.right = new Node(5);
root2.right.left = new Node(-6);
root2.right.right = new Node(2);

console.log(findMaxSubtreeSum(root2)); // Output: 7
```

<hr/>

💡 **Question-2:** Construct the BST (Binary Search Tree) from its given level order traversal.

Example:

Input: arr[] = {7, 4, 12, 3, 6, 8, 1, 5, 10}

Output: BST:

            7

         /    \

        4     12

      /  \     /

      3   6  8

     /    /     \

     1    5      10

💬 **Solution-2:**

```js
class Node {
  constructor(value) {
    this.value = value;
    this.left = null;
    this.right = null;
  }
}

function constructBSTFromLevelOrder(arr) {
  if (arr.length === 0) {
    return null;
  }

  const root = new Node(arr[0]);
  const queue = [root];
  let i = 1;

  while (i < arr.length) {
    const currentNode = queue.shift();

    // creating the left child node if it exists
    if (i < arr.length && arr[i] < currentNode.value) {
      currentNode.left = new Node(arr[i]);
      queue.push(currentNode.left);
      i++;
    }

    // creating the right child node if it exists
    if (i < arr.length && arr[i] > currentNode.value) {
      currentNode.right = new Node(arr[i]);
      queue.push(currentNode.right);
      i++;
    }
  }

  return root;
}

// Example:
const arr = [7, 4, 12, 3, 6, 8, 1, 5, 10];

const root = constructBSTFromLevelOrder(arr);

// function to perform an inorder traversal of the BST (for verification)
function inorderTraversal(node) {
  if (node === null) {
    return;
  }

  inorderTraversal(node.left);
  console.log(node.value);
  inorderTraversal(node.right);
}

inorderTraversal(root);
```

<hr/>

💡 **Question-3:** Given an array of size n. The problem is to check whether the given array can represent the level order traversal of a Binary Search Tree or not.

Examples:

Input1 : arr[] = {7, 4, 12, 3, 6, 8, 1, 5, 10}

Output1 : Yes

For the given arr[], the Binary Search Tree is:

            7

         /    \

       4     12

     /  \     /

    3   6  8

    /    /     \

    1    5      10

Input2 : arr[] = {11, 6, 13, 5, 12, 10}

Output2 : No

The given arr[] does not represent the level order traversal of a BST.

💬 **Solution-3:**

```js
function canRepresentBST(arr) {
  if (arr.length === 0) {
    return true;
  }

  const n = arr.length;
  let i;

  for (i = 1; i < n; i++) {
    if (arr[i] > arr[0]) {
      break;
    }
  }

  for (let j = i; j < n; j++) {
    if (arr[j] < arr[0]) {
      return false;
    }
  }

  let leftResult = true;
  let rightResult = true;

  // recursively checking if the left subtree can represent a BST
  if (i > 1) {
    leftResult = canRepresentBST(arr.slice(1, i));
  }

  // recursively checking if the right subtree can represent a BST
  if (i < n) {
    rightResult = canRepresentBST(arr.slice(i));
  }

  // returning true only if both left and right subtrees can represent a BST
  return leftResult && rightResult;
}

// Examples:
const arr1 = [7, 4, 12, 3, 6, 8, 1, 5, 10];
console.log(canRepresentBST(arr1)); // Output: true

const arr2 = [11, 6, 13, 5, 12, 10];
console.log(canRepresentBST(arr2)); // Output: false
```

<hr/>