# Assignment-13 Questions & Solutions

💡 **Question-1:** Given two linked list of the same size, the task is to create a new linked list using those linked lists. The condition is that the greater node among both linked list will be added to the new linked list.

Examples:

```
Input: list1 = 5->2->3->8
list2 = 1->7->4->5
Output: New list = 5->7->4->8

Input:list1 = 2->8->9->3
list2 = 5->3->6->4
Output: New list = 5->8->9->4
```

💬 **Solution-1:**

```js
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedList {
  constructor() {
    this.head = null;
  }

  addNode(value) {
    const newNode = new Node(value);
    if (this.head === null) {
      this.head = newNode;
    } else {
      let current = this.head;
      while (current.next !== null) {
        current = current.next;
      }
      current.next = newNode;
    }
  }
}

function createNewLinkedList(list1, list2) {
  if (!list1.head || !list2.head) {
    return null;
  }

  const newList = new LinkedList();
  let current1 = list1.head;
  let current2 = list2.head;
  while (current1 !== null && current2 !== null) {
    if (current1.value >= current2.value) {
      newList.addNode(current1.value);
      current1 = current1.next;
    } else {
      newList.addNode(current2.value);
      current2 = current2.next;
    }
  }

  while (current1 !== null) {
    newList.addNode(current1.value);
    current1 = current1.next;
  }

  while (current2 !== null) {
    newList.addNode(current2.value);
    current2 = current2.next;
  }
  return newList;
}

// Example:
const list1 = new LinkedList();
list1.addNode(5);
list1.addNode(2);
list1.addNode(3);
list1.addNode(8);

const list2 = new LinkedList();
list2.addNode(1);
list2.addNode(7);
list2.addNode(4);
list2.addNode(5);

const newList = createNewLinkedList(list1, list2);

// Printing the new linked list
let current = newList.head;
while (current !== null) {
  console.log(current.value);
  current = current.next;
}

```

<hr/>

💡 **Question-2:** Write a function that takes a list sorted in non-decreasing order and deletes any duplicate nodes from the list. The list should only be traversed once.

For example if the linked list is 11->11->11->21->43->43->60 then removeDuplicates() should convert the list to 11->21->43->60.

Examples:

```
Input:
LinkedList: 
11->11->11->21->43->43->60
Output:
11->21->43->60

Input:
LinkedList: 
10->12->12->25->25->25->34
Output:
10->12->25->34
```

💬 **Solution-2:**

```js
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedList {
  constructor() {
    this.head = null;
  }

  addNode(value) {
    const newNode = new Node(value);
    if (this.head === null) {
      this.head = newNode;
    } else {
      let current = this.head;
      while (current.next !== null) {
        current = current.next;
      }
      current.next = newNode;
    }
  }

  removeDuplicates() {
    if (!this.head) {
      return;
    }

    let current = this.head;

    while (current.next !== null) {
      if (current.value === current.next.value) {
        current.next = current.next.next;
      } else {
        current = current.next;
      }
    }
  }

  printList() {
    let current = this.head;
    const values = [];
    while (current !== null) {
      values.push(current.value);
      current = current.next;
    }
    console.log(values.join("->"));
  }
}

// Example:
const list = new LinkedList();
list.addNode(11);
list.addNode(11);
list.addNode(11);
list.addNode(21);
list.addNode(43);
list.addNode(43);
list.addNode(60);

list.removeDuplicates();
list.printList(); // Output: 11->21->43->60

```

<hr/>

💡 **Question-3:** Given a linked list of size **N**. The task is to reverse every **k** nodes (where k is an input to the function) in the linked list. If the number of nodes is not a multiple of *k* then left-out nodes, in the end, should be considered as a group and must be reversed (See Example 2 for clarification).

Examples:

```
Input:
LinkedList: 1->2->2->4->5->6->7->8
K = 4
Output:4 2 2 1 8 7 6 5
Explanation:
The first 4 elements 1,2,2,4 are reversed first
and then the next 4 elements 5,6,7,8. Hence, the
resultant linked list is 4->2->2->1->8->7->6->5.

Input:
LinkedList: 1->2->3->4->5
K = 3
Output:3 2 1 5 4
Explanation:
The first 3 elements are 1,2,3 are reversed
first and then elements 4,5 are reversed.Hence,
the resultant linked list is 3->2->1->5->4.
```

💬 **Solution-3:**

```js
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedList {
  constructor() {
    this.head = null;
  }

  addNode(value) {
    const newNode = new Node(value);
    if (this.head === null) {
      this.head = newNode;
    } else {
      let current = this.head;
      while (current.next !== null) {
        current = current.next;
      }
      current.next = newNode;
    }
  }

  reverseKNodes(k) {
    if (!this.head || k === 0 || k === 1) {
      return;
    }

    let current = this.head;
    let previous = null;

    while (current !== null) {
      let count = 0;
      let temp = null;
      let reversedHead = current;

      // Reverse k nodes
      while (current !== null && count < k) {
        temp = current.next;
        current.next = previous;
        previous = current;
        current = temp;
        count++;
      }

      if (count === k) {
        if (!this.head) {
          this.head = previous;
        } else {
          reversedHead.next = current;
          let currentHead = reversedHead;
          reversedHead = previous;
          previous = null;

          if (currentHead !== null) {
            while (currentHead.next !== null) {
              currentHead = currentHead.next;
            }
            currentHead.next = reversedHead;
          }
        }
      } else {
        current = previous;
        previous = null;
        while (current !== null) {
          temp = current.next;
          current.next = previous;
          previous = current;
          current = temp;
        }
        let currentHead = previous;

        // Connecting the previous group to the remaining reversed nodes
        if (currentHead !== null) {
          while (currentHead.next !== null) {
            currentHead = currentHead.next;
          }
          currentHead.next = reversedHead;
        }
      }
    }
  }

  printList() {
    let current = this.head;
    const values = [];
    while (current !== null) {
      values.push(current.value);
      current = current.next;
    }
    console.log(values.join(" "));
  }
}

// Example:
const list = new LinkedList();
list.addNode(1);
list.addNode(2);
list.addNode(2);
list.addNode(4);
list.addNode(5);
list.addNode(6);
list.addNode(7);
list.addNode(8);

const k = 4;
list.reverseKNodes(k);
list.printList(); // Output:4 2 2 1 8 7 6 5

```

<hr/>

💡 **Question-4:** Given a linked list, write a function to reverse every alternate k nodes (where k is an input to the function) in an efficient way. Give the complexity of your algorithm.

Example:

```
Inputs:   1->2->3->4->5->6->7->8->9->NULL and k = 3
Output:   3->2->1->4->5->6->9->8->7->NULL.
```

💬 **Solution-4:**

```js
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedList {
  constructor() {
    this.head = null;
  }

  addNode(value) {
    const newNode = new Node(value);
    if (this.head === null) {
      this.head = newNode;
    } else {
      let current = this.head;
      while (current.next !== null) {
        current = current.next;
      }
      current.next = newNode;
    }
  }

  reverseAlternateKNodes(k) {
    if (!this.head || k <= 1) {
      return;
    }

    let current = this.head;
    let previous = null;
    let count = 0;
    let reversedHead = null;
    let reversedTail = null;
    let reverseFlag = true;

    while (current !== null) {
      let temp = null;

      if (reverseFlag) {
        count = 0;
        reversedHead = current;
        while (current !== null && count < k) {
          temp = current.next;
          current.next = previous;
          previous = current;
          current = temp;
          count++;
        }
        if (!reversedTail) {
          reversedTail = reversedHead;
        }
        if (reversedTail) {
          reversedTail.next = previous;
        }
        reversedTail = reversedHead;
        previous = null;
        reverseFlag = false;
      } else {
        // Skip k nodes
        count = 0;
        while (current !== null && count < k) {
          previous = current;
          current = current.next;
          count++;
        }
        reverseFlag = true;
      }
    }
    this.head = reversedHead;
  }

  printList() {
    let current = this.head;
    const values = [];
    while (current !== null) {
      values.push(current.value);
      current = current.next;
    }
    console.log(values.join("->"));
  }
}

// Example:
const list = new LinkedList();
list.addNode(1);
list.addNode(2);
list.addNode(3);
list.addNode(4);
list.addNode(5);
list.addNode(6);
list.addNode(7);
list.addNode(8);
list.addNode(9);

const k = 3;
list.reverseAlternateKNodes(k);
list.printList(); // Output:   3->2->1->4->5->6->9->8->7

```

<hr/>

💡 **Question-5:** Given a linked list and a key to be deleted. Delete last occurrence of key from linked. The list may have duplicates.

Examples:

```
Input:   1->2->3->5->2->10, key = 2
Output:  1->2->3->5->10
```

💬 **Solution-5:**

```js
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedList {
  constructor() {
    this.head = null;
  }

  addNode(value) {
    const newNode = new Node(value);
    if (this.head === null) {
      this.head = newNode;
    } else {
      let current = this.head;
      while (current.next !== null) {
        current = current.next;
      }
      current.next = newNode;
    }
  }

  deleteLastOccurrence(key) {
    if (!this.head) {
      return;
    }

    let current = this.head;
    let lastOccurrence = null;
    let prevLastOccurrence = null;

    while (current !== null) {
      if (current.value === key) {
        lastOccurrence = current;
        prevLastOccurrence = null;
      }
      if (current.next !== null && current.next.value === key) {
        prevLastOccurrence = current;
      }
      current = current.next;
    }

    if (lastOccurrence !== null) {
      if (prevLastOccurrence === null) {
        this.head = lastOccurrence.next;
      } else {
        prevLastOccurrence.next = lastOccurrence.next;
      }
    }
  }

  printList() {
    let current = this.head;
    const values = [];
    while (current !== null) {
      values.push(current.value);
      current = current.next;
    }
    console.log(values.join("->"));
  }
}

// Example:
const list = new LinkedList();
list.addNode(1);
list.addNode(2);
list.addNode(3);
list.addNode(5);
list.addNode(2);
list.addNode(10);

const key = 2;
list.deleteLastOccurrence(key);
list.printList(); // Output:  1->2->3->5->10

```

<hr/>

💡 **Question-6:** Given two sorted linked lists consisting of **N** and **M** nodes respectively. The task is to merge both of the lists (in place) and return the head of the merged list.

Examples:

```
Input: a: 5->10->15, b: 2->3->20
Output: 2->3->5->10->15->20

Input: a: 1->1, b: 2->4
Output: 1->1->2->4
```

💬 **Solution-6:**

```js
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

function mergeSortedLists(a, b) {
  if (!a) {
    return b;
  }
  if (!b) {
    return a;
  }

  let head = null;
  let tail = null;

  if (a.value <= b.value) {
    head = a;
    a = a.next;
  } else {
    head = b;
    b = b.next;
  }
  tail = head;

  while (a && b) {
    if (a.value <= b.value) {
      tail.next = a;
      a = a.next;
    } else {
      tail.next = b;
      b = b.next;
    }
    tail = tail.next;
  }

  if (a) {
    tail.next = a;
  } else {
    tail.next = b;
  }

  return head;
}

// Example:
const list1 = new Node(5);
list1.next = new Node(10);
list1.next.next = new Node(15); 

const list2 = new Node(2);
list2.next = new Node(3);
list2.next.next = new Node(20); // Input: a: 5->10->15, b: 2->3->20

const mergedList = mergeSortedLists(list1, list2);
printList(mergedList); // Output: 2->3->5->10->15->20

function printList(head) {
  const values = [];
  let current = head;
  while (current !== null) {
    values.push(current.value);
    current = current.next;
  }
  console.log(values.join("->"));
}

```

<hr/>

💡 **Question-7:** Given a **Doubly Linked List**, the task is to reverse the given Doubly Linked List.

Example:

```
Original Linked list 10 8 4 2
Reversed Linked list 2 4 8 10
```

💬 **Solution-7:**

```js
class Node {
  constructor(value) {
    this.value = value;
    this.prev = null;
    this.next = null;
  }
}

class DoublyLinkedList {
  constructor() {
    this.head = null;
  }

  addNode(value) {
    const newNode = new Node(value);
    if (this.head === null) {
      this.head = newNode;
    } else {
      let current = this.head;
      while (current.next !== null) {
        current = current.next;
      }
      current.next = newNode;
      newNode.prev = current;
    }
  }

  reverse() {
    if (!this.head || !this.head.next) {
      return;
    }

    let current = this.head;
    let temp = null;
    while (current !== null) {
      temp = current.prev;
      current.prev = current.next;
      current.next = temp;
      current = current.prev;
    }

    if (temp !== null) {
      this.head = temp.prev;
    }
  }

  printList() {
    let current = this.head;
    const values = [];
    while (current !== null) {
      values.push(current.value);
      current = current.next;
    }
    console.log(values.join(" "));
  }
}

// Example:
const list = new DoublyLinkedList();
list.addNode(10);
list.addNode(8);
list.addNode(4);
list.addNode(2);

console.log("Original Linked list:");
list.printList(); // Original Linked list: 10 8 4 2

list.reverse();

console.log("Reversed Linked list:");
list.printList(); // Reversed Linked list: 2 4 8 10

```

<hr/>

💡 **Question-8:** Given a doubly linked list and a position. The task is to delete a node from given position in a doubly linked list.

Examples:

```
Input:
LinkedList = 1 <--> 3 <--> 4
x = 3
Output:1 3
Explanation:After deleting the node at
position 3 (position starts from 1),
the linked list will be now as 1->3.

Input:
LinkedList = 1 <--> 5 <--> 2 <--> 9
x = 1
Output:5 2 9
```

💬 **Solution-8:**

```js
class Node {
  constructor(value) {
    this.value = value;
    this.prev = null;
    this.next = null;
  }
}

class DoublyLinkedList {
  constructor() {
    this.head = null;
  }

  addNode(value) {
    const newNode = new Node(value);
    if (this.head === null) {
      this.head = newNode;
    } else {
      let current = this.head;
      while (current.next !== null) {
        current = current.next;
      }
      current.next = newNode;
      newNode.prev = current;
    }
  }

  deleteNode(position) {
    if (!this.head) {
      return;
    }

    let current = this.head;
    let count = 1;
    
    while (current !== null && count < position) {
      current = current.next;
      count++;
    }

    if (current === null) {
      return;
    }

    if (current === this.head) {
      this.head = current.next;
      if (this.head !== null) {
        this.head.prev = null;
      }
    } else {
      current.prev.next = current.next;
      if (current.next !== null) {
        current.next.prev = current.prev;
      }
    }
  }

  printList() {
    let current = this.head;
    const values = [];
    while (current !== null) {
      values.push(current.value);
      current = current.next;
    }
    console.log(values.join(" "));
  }
}

// Example:
const list = new DoublyLinkedList();
list.addNode(1);
list.addNode(5);
list.addNode(2);
list.addNode(9);

console.log("Original Linked list:");
list.printList();

const position = 1;
list.deleteNode(position);

console.log("Linked list after deleting node at position", position);
list.printList();

```

<hr/>