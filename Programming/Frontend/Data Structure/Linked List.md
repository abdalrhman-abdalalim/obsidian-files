### **Arrays vs. Linked Lists: Advantages & Disadvantages**

#### **Arrays**

✅ **Advantages:**

- **Fast Access:** Accessing any element by index is very efficient (**O(1) time complexity**).

❌ **Disadvantages:**

- **Fixed Size:** The size of an array is predetermined and cannot be easily changed.
- **Costly Insertion & Deletion:**
    - If we have `[1,2,3]` and delete `2`, element `3` has to **shift** left.
    - In large arrays, this **shifting operation** increases memory usage and slows performance (**O(n) complexity**).
- **Continuous Memory Allocation:** The array elements are stored in contiguous memory locations, which can lead to **memory fragmentation issues** when resizing.

---

#### **Linked Lists**

✅ **Advantages:**

- **Dynamic Size:** Can grow and shrink dynamically, unlike arrays.
- **Efficient Insertions & Deletions:** Adding/removing elements does not require shifting other elements (**O(1) in optimal cases**).
- **Non-contiguous Memory Allocation:** Each node is stored independently, making it memory-efficient when dealing with frequent insertions.

❌ **Disadvantages:**

- **Slow Element Access:** Unlike arrays, accessing an element requires traversing the list (**O(n) complexity**).
- **Extra Memory Usage:** Each node stores a reference (or pointer) to the next node, which increases memory consumption.

---
### **Explanation of the Linked List Code**

#### **1️⃣ `Node` Class**

```js
class Node {   
	constructor(data, next = null) {     
		this.head = data;     this.next = next;   
} }
```

- Represents a **single element (node)** in the linked list.
- Each node stores:
    - `head`: The actual **data**.
    - `next`: A **reference** to the next node (or `null` if it's the last node).

---
#### 2️⃣ `LinkedList` Class

```js
class LinkedList {
  constructor() {
    this.head = null;
    this.size = 0;
  }
}
```

- **`this.head`**: Points to the first node of the linked list.
- **`this.size`**: Tracks the number of nodes.

---
#### 3️⃣ `addFirst(data)` - Add Element at the Beginning

```js
addFirst(data) {
  this.head = new Node(data, this.head);
  this.size++;
}

```

- Creates a new node and sets its `next` pointer to the **current head**.
- Updates `this.head` to the new node.

✅ **Time Complexity:** **O(1)**

---
#### 4️⃣ `addLast(data)` - Add Element at the End

```js
addLast(data) {
  if (!this.head) {
    this.head = new Node(data);
  } else {
    let current = this.head;
    while (current.next) {
      current = current.next;
    }
    current.next = new Node(data);
  }
  this.size++;
}

```

- If the list is empty, set `this.head` to the new node.
- Otherwise, **traverse** the list to the last node and attach the new node.

✅ **Time Complexity:** **O(n)** (traverses the entire list)

---
#### 5️⃣ `addElementInIndex(data, index)` - Insert at a Specific Index

```js
addElementInIndex(data, index) {
  if (index < 0 || index > this.size) return;
  if (index == 0) return this.addFirst(data);

  let node = new Node(data);
  let prev;
  let current = this.head;
  let counter = 0;

  while (counter < index) {
    counter++;
    prev = current;
    current = current.next;
  }
  prev.next = node;
  node.next = current;
  this.size++;
}

```

- If `index == 0`, use `addFirst()`.
- Otherwise, traverse to `index - 1`, update pointers, and insert the new node.

✅ **Time Complexity:** **O(n)** (traverses up to `index`)

---
#### 6️⃣ `deleteElementInIndex(index)` - Delete at a Specific Index

```js
deleteElementInIndex(index) {
  if (index < 0 || index > this.size) return;

  let prev;
  let current = this.head;
  let counter = 0;

  while (counter < index) {
    counter++;
    prev = current;
    current = current.next;
  }
  console.log(current);
  console.log(prev);
  prev.next = current.next;
}

```

- Traverses to `index - 1` and updates `prev.next` to skip `current`, effectively deleting it.

✅ **Time Complexity:** **O(n)** (traverses up to `index`)

---
#### 7️⃣ `getAllData()` - Print All Elements

```js
getAllData() {
  let current = this.head;
  while (current) {
    console.log(current.head);
    current = current.next;
  }
}

```

- Traverses the list and prints each node’s data.

✅ **Time Complexity:** **O(n)**


