# Linked List in C

## Introduction
A linked list is a linear data structure where elements are stored in nodes, and each node points to the next node in the sequence. Unlike arrays, linked lists do not have a fixed size and can dynamically allocate memory.

## Types of Linked Lists
1. **Singly Linked List** - Each node contains data and a pointer to the next node.
2. **Doubly Linked List** - Each node contains data, a pointer to the next node, and a pointer to the previous node.
3. **Circular Linked List** - The last node points back to the first node, forming a loop.

## Structure of a Node
In C, a node for a singly linked list can be represented as:

```c
struct Node {
    int data;
    struct Node* next;
};
```

## Basic Operations

### 1. Creating a Node
```c
#include <stdio.h>
#include <stdlib.h>

struct Node* createNode(int value) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = value;
    newNode->next = NULL;
    return newNode;
}
```

### 2. Insertion
- **At the beginning**
```c
void insertAtBeginning(struct Node** head, int value) {
    struct Node* newNode = createNode(value);
    newNode->next = *head;
    *head = newNode;
}
```
- **At the end**
```c
void insertAtEnd(struct Node** head, int value) {
    struct Node* newNode = createNode(value);
    if (*head == NULL) {
        *head = newNode;
        return;
    }
    struct Node* temp = *head;
    while (temp->next != NULL) {
        temp = temp->next;
    }
    temp->next = newNode;
}
```

### 3. Deletion
- **From the beginning**
```c
void deleteFromBeginning(struct Node** head) {
    if (*head == NULL) return;
    struct Node* temp = *head;
    *head = (*head)->next;
    free(temp);
}
```
- **From the end**
```c
void deleteFromEnd(struct Node** head) {
    if (*head == NULL) return;
    struct Node* temp = *head, *prev = NULL;
    while (temp->next != NULL) {
        prev = temp;
        temp = temp->next;
    }
    if (prev != NULL)
        prev->next = NULL;
    else
        *head = NULL;
    free(temp);
}
```

### 4. Traversing the Linked List
```c
void printList(struct Node* head) {
    struct Node* temp = head;
    while (temp != NULL) {
        printf("%d -> ", temp->data);
        temp = temp->next;
    }
    printf("NULL\n");
}
```

## Advantages of Linked List
- Dynamic memory allocation (no need to specify size in advance)
- Efficient insertions and deletions compared to arrays

## Disadvantages of Linked List
- Requires extra memory for pointers
- Slower access time (O(n) complexity for search)

## Conclusion
Linked lists are useful in scenarios where frequent insertions and deletions are required. They provide flexibility but at the cost of extra memory usage. Understanding linked lists is fundamental for mastering data structures in C.
