## LinkedList(SinglyLinkedList)
### what if we have both tail and Head
```js
class Node {
    constructor(value){
        this.value = value;
        this.next = null;
    }
}
 
class LinkedList {
    constructor(value) {
        const newNode = new Node(value);
        this.head = newNode;
        this.tail = this.head;
        this.length = 1;
    }

    printList() {
        let temp = this.head;
        while (temp !== null) {
            console.log(temp.value);
            temp = temp.next;
        }
    }

    getHead() {
        if (this.head === null) {
            console.log("Head: null");
        } else {
            console.log("Head: " + this.head.value);
        }
    }

    getTail() {
        if (this.tail === null) {
            console.log("Tail: null");
        } else {
            console.log("Tail: " + this.tail.value);
        }
    }

    getLength() {
        console.log("Length: " + this.length);
    }

    makeEmpty() {
        this.head = null;
        this.tail = null;
        this.length = 0;
    }
 
    push(value) {
        const newNode = new Node(value);
        if (!this.head) {
            this.head = newNode;
            this.tail = newNode;
        } else {
            this.tail.next = newNode;
            this.tail = newNode;
        }
        this.length++;
        return this;
    }
 
    pop() {
        if (this.length === 0) return undefined;
        let temp = this.head;
        let pre = this.head;
        while (temp.next) {
            pre = temp;
            temp = temp.next;
        }
        this.tail = pre;
        this.tail.next = null;
        this.length--;
        if (this.length === 0) {
            this.head = null;
            this.tail = null;
        }
        return temp;
    }
 
    unshift(value) {
        const newNode = new Node(value);
        if (!this.head) {
            this.head = newNode;
            this.tail = newNode;
        } else {
            newNode.next = this.head;
            this.head = newNode;
        }
        this.length++;
        return this;
    }
 
    shift() {
        if (this.length === 0) return undefined;
        let temp = this.head;
        this.head = this.head.next;
        this.length--;
        if (this.length === 0) {
            this.tail = null;
        }
        temp.next = null;
        return temp;
    }
 
    get(index) {
        if (index < 0 || index >= this.length) return undefined;
        let temp = this.head;
        for (let i = 0; i < index; i++) {
            temp = temp.next;
        }
        return temp;
    }
 
    set(index, value) {
        let temp = this.get(index);
        if (temp) {
            temp.value = value;
            return true;
        }
        return false;
    }
 
    insert(index, value) {
        if (index < 0 || index > this.length) return false;
        if (index === this.length) return this.push(value);
        if (index === 0) return this.unshift(value);
        
        const newNode = new Node(value);
        const temp = this.get(index - 1);
        newNode.next = temp.next;
        temp.next = newNode;
        this.length++;
        return true;
    }
 
    remove(index) {
        if (index < 0 || index >= this.length) return undefined;
        if (index === 0) return this.shift();
        if (index === this.length - 1) return this.pop();

        const before = this.get(index - 1);
        const temp = before.next;

        before.next = temp.next;
        temp.next = null;
        this.length--;
        return temp;
    }

    reverse() {
        let temp = this.head;
        this.head = this.tail;
        this.tail = temp;
        let next = temp.next;
        let prev = null;
        for (let i = 0; i < this.length; i++) {
            next = temp.next;
            temp.next = prev;
            prev = temp;
            temp = next;
        }
    }  

}
function test() {
    let myLinkedList = new LinkedList(1);
    myLinkedList.push(2);
    myLinkedList.push(3);
    myLinkedList.push(4);

    console.log("LL before reverse():");
    myLinkedList.printList();

    myLinkedList.reverse();

    console.log("\nLL after reverse():");
    myLinkedList.printList();
}

test();
```
#### now let's have some problems asked in interviews
##### `findMiddleNode()`:
```js
findMiddleNode() {
  if (!this.head) return null;

  let slow = this.head;
  let fast = this.head;

  while (fast && fast.next) {
    slow = slow.next;
    fast = fast.next.next;
  }

  return slow;
}
//How It Works:
//`slow` moves one step at a time. 
//`fast` moves two steps at a time. 
//When `fast` reaches the end, `slow` is in the **middle**.
```
#### `hasLoop()`
```js
hasLoop() {
  let slow = this.head;
  let fast = this.head;

  while (fast && fast.next) {
    slow = slow.next;
    fast = fast.next.next;

    if (slow === fast) {
      return true; // Cycle detected
    }
  }

  return false; // No cycle
}
// If there's a cycle, they will eventually meet inside the loop.
// If the list has an end (null), the loop will exit and return false.
```
#### finds the k-th element from the end
```js
findKthelementfromend(k) {
    let current = this.head;
    let listofelement = [];

    while (current) {
        listofelement.push(current.value); // Store all values
        current = current.next;
    }

    let nooflement = listofelement.length;
    return listofelement[nooflement - k]; // Return k-th from end
}

```
- It creates an array of all values (extra space = O(n))
- Then accesses the `k-th` from the end using length - k
###### ❌ Issues:
1. **Uses O(n) extra space** — for storing all elements
2. Doesn’t handle edge cases like `k <= 0` or `k > length`
3. Slightly less efficient than it could be
##### Optimized Version (Two Pointer Technique — O(1) space, O(n) time):
```js
findKthFromEnd(k) {
    if (k <= 0) return undefined;
    let slow = this.head;
    let fast = this.head;
    // Move fast pointer k steps ahead
    for (let i = 0; i < k; i++) {
        if (fast === null) return undefined; // k is greater than list length
        fast = fast.next;
    }
    // Move both pointers until fast reaches the end
    while (fast) {
        slow = slow.next;
        fast = fast.next;
    }
    return slow?.value; // This is the k-th node from the end
}
```
##### remove duplicate values from a singly linked list\
```js
removeDuplicates() {
    let current = this.head;
    let prev = null;
    let uniqueValues = new Set();

    while (current) {
        if (uniqueValues.has(current.value)) {
            prev.next = current.next;
            this.length--; // optional if you're tracking length
        } else {
            uniqueValues.add(current.value);
            prev = current;
        }
        current = current.next;
    }

    return this;
}

```
##### Partition a Linked List Around a Value x
Goal: Given a linked list and a value x, rearrange the nodes such that:
All nodes less than `x` come before nodes greater than or equal to `x`
The relative order of nodes in each partition should be preserved
``` ini
head = 3 → 5 → 8 → 5 → 10 → 2 → 1
x = 5
// Output:
3 → 2 → 1 → 5 → 8 → 5 → 10

```
##### Approach: Two Pointers + Dummy Lists
We use **two separate lists**:
1. One list for **nodes < x**
2. One list for **nodes ≥ x**
```js
partition(x) {
    let lessHead = new Node(0);   // dummy head for < x
    let greaterHead = new Node(0); // dummy head for >= x
    let less = lessHead;
    let greater = greaterHead;
    let current = this.head;
    while (current) {
        if (current.value < x) {
            less.next = current;
            less = less.next;// move pointer forward to prepare for next insertion
        } else {
            greater.next = current;
            greater = greater.next;
        }
        current = current.next;
    }
    greater.next = null;        // end of new list
    less.next = greaterHead.next;  // connect less list to greater list

    this.head = lessHead.next;     // update real head

    return this;
}

```
##### Reverse Between Two Positions in a Singly Linked List
**Problem:** Given a singly linked list, reverse the nodes from position `left` to `right`. Do it in-place and in one pass.
```js
reverseBetween(left, right) {
    if (!this.head || left === right) return this;

    let dummy = new Node(0);
    dummy.next = this.head;
    let prev = dummy;

    // 1. Move `prev` to one node before `left`
    for (let i = 1; i < left; i++) {
        prev = prev.next;
    }

    // 2. Reverse the sublist from `left` to `right`
    let current = prev.next;
    let nextNode = null;

    for (let i = 0; i < right - left; i++) {
        nextNode = current.next;
        current.next = nextNode.next;
        nextNode.next = prev.next;
        prev.next = nextNode;
    }

    // 3. Update head if needed
    this.head = dummy.next;
    return this;
}

```