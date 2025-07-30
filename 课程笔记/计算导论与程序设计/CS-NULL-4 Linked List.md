## Chapter 22: Linked List
### **Chapter Objectives 任务目标**

- Understand the **Array** and **Dynamic Array** concepts
    
- Learn about **Singly Linked List** (structure, creation, insertion, deletion)
    
- Explore **Doubly Linked List**
    
- Understand **Ordered Linked List**
    
- Study **Merging Linked Lists**
    
- Get familiar with the **Skip List**
    
- Discuss the **Advantages and Disadvantages** of Linked Lists
    

---

### **1. Array and Dynamic Array**

#### **Array (静态数组)**

- A **linear table** is a finite sequence of elements with the same data type.
    
    - Example: (a1, a2, ... an)
        
    - A linear table can be represented by arrays in programming.
        
- **Storage Structure of Array**:
    
    - Fixed-length linear table.
        

#### **Dynamic Array (动态数组)**

- Unlike static arrays, **dynamic arrays** can expand or shrink based on the data stored.
    
- This requires allocating memory dynamically when the array is resized.
    

---

### **2. Introduction to Linked List**

#### **What is a Linked List?**

- A **linked list** is a data structure where each element (node) contains:
    
    - **Data**: The value stored in the node.
        
    - **Pointer**: A reference to the next node in the list.
        
- **Types of Linked Lists**:
    
    - **Singly Linked List**: Each node points only to the next node.
        
    - **Doubly Linked List**: Each node points to both the next and previous nodes.
        
    - **Circular Linked List**: The last node points to the first node, forming a circular structure.
        

---

### **3. Singly Linked List**

#### **Singly Linked List Structure**

- A **node** typically contains two parts:
    
    - **Data**: Stores the value.
        
    - **Pointer (pNext)**: Points to the next node.
        

#### **Creating a Singly Linked List Node**

- Allocate memory for the node and assign the data value.
    
- Initialize the `pNext` pointer to NULL (for the last node).
    

```c
struct Node {
  struct Data data;
  struct Node* pNext;
};

struct Node* createNode(struct Data* data) {
  struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
  newNode->data = *data;
  newNode->pNext = NULL;
  return newNode;
}
```

#### **Inserting a Node**

- To insert at the head, create a new node, point its `pNext` to the current head, and update the head to the new node.
    

```c
struct Node* insertHead(struct Node* head, struct Data* data) {
  struct Node* newNode = createNode(data);
  newNode->pNext = head;
  return newNode;
}
```

#### **Traversing a Linked List**

- To find or update a node, traverse the list starting from the head and check each node's data.
    

---

### **4. Doubly Linked List**

#### **Doubly Linked List Structure**

- A doubly linked list node contains:
    
    - **Data**: Stores the value.
        
    - **Pointer (pPrev)**: Points to the previous node.
        
    - **Pointer (pNext)**: Points to the next node.
        

#### **Creating and Inserting Nodes in Doubly Linked List**

- When inserting or deleting, pointers to both the previous and next nodes need to be updated.
    

```c
struct Node {
  struct Data data;
  struct Node* pPrev;
  struct Node* pNext;
};

struct Node* createNode(struct Data* data) {
  struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
  newNode->data = *data;
  newNode->pPrev = NULL;
  newNode->pNext = NULL;
  return newNode;
}
```

---

### **5. Ordered Linked List**

#### **Ordered Linked List**

- **Unordered Linked List**: Standard linked list without any specific ordering.
    
- **Ordered Linked List**: Nodes are arranged in sorted order, allowing for faster searches and more efficient merge operations.
    

#### **Advantages**:

- **Binary Search Optimization**: Efficient searching in ordered lists using binary search principles (via skip lists).
    
- **Duplicate Detection**: Easily detect duplicates when inserting nodes.
    
- **Merging Sorted Lists**: Merging two ordered lists can be done in O(n) time.
    

---

### **6. Merging Linked Lists**

#### **Merging Two Ordered Linked Lists**

- To merge two sorted linked lists, compare their elements and insert them in ascending order.
    

```c
struct Node* merge(struct Node* pHead1, struct Node* pHead2) {
  struct Node* result = NULL;
  struct Node* node = NULL;
  
  // Add head nodes based on comparison
  if (pHead1->data.a > pHead2->data.a)
    addNext(&result, &pHead2);
  else
    addNext(&result, &pHead1);
  
  // Merge nodes one by one
  node = result;
  while (pHead1 != NULL && pHead2 != NULL) {
    if (pHead1->data.a > pHead2->data.a)
      node = addNext(&node, &pHead2);
    else
      node = addNext(&node, &pHead1);
  }

  // Add the remaining nodes
  if (pHead1 == NULL)
    addNext(&node, &pHead2);
  if (pHead2 == NULL)
    addNext(&node, &pHead1);

  return result;
}
```

---

### **7. Skip List**

#### **What is a Skip List?**

- A **skip list** is a multi-level linked list that allows for fast searching by jumping over intermediate elements. This structure is probabilistic and aims to achieve O(log n) search time for insertion, deletion, and search operations.
    链表并不支持使用下标去访问，因此折半搜索失效了。不能一下子访问中间值，但是链表可以随意的链接。通过添加节点指向中间位置。二叉树

#### **Skip List Structure**

- Each node in the skip list can have multiple levels:
    
    - **pNext**: Points to the next node at the same level.
        
    - **pDown**: Points to the corresponding node in the level below.
        

#### **Skip List Creation**

- A skip list node is created for each level. Nodes at higher levels help skip over nodes at lower levels, improving search efficiency.
    

```c
struct SkipNode {
  int level;
  struct Node* pData;
  struct SkipNode* pDown;
  struct SkipNode* pNext;
};
```

#### **Insertion in Skip List**

- Insert nodes into the skip list, linking nodes across levels to ensure faster search times.
    

---

### **8. Advantages and Disadvantages of Linked Lists**

#### **Advantages**:

- Dynamic size: Can grow or shrink as needed.
    
- Efficient insertions and deletions (especially at the head or in the middle).
    

#### **Disadvantages**:

- **Memory Overhead**: Each node requires extra memory for pointers.
    
- **No Random Access**: Cannot use index-based access like arrays. Traversing is needed for access.
    
- **Complexity**: Operations like insertion and deletion require careful pointer adjustments, which increases complexity.
    
