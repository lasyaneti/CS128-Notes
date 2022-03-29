# 03/09/2022: Dynamic Structures

## Limitations of VectorInt
- push_back when size = capacity is slightly tedious
- Push to front = copy all elements one index ahead and add element at open index 1
- Fast to get item at index, slow to insert or delete item

## Sequence of Nodes
```cpp
struct Node {
    int data;
    Node* next;
}

Node* head = new Node(7);
// same as (*head).next
head->next = new Node(11);
```

### Adding to the end of linked list
DO NOT USE HEAD TO TRAVERSE BECAUSE IT IS OUR SINGLE ENTRY POINT INTO THE LIST, WE CANNOT AFFORD TO LOSE IT!!
```cpp
Node* curr_node = head;
while (curr_node != nullptr) {
    curr_node = curr_next->next;
}
curr_node->next = new Node(8);
```
**Faster way to do this: store a pointer to the tail**
```cpp
Node* temp = new Node(9);
tail->next = temp;
tail = temp;
```

### Adding at a specific position
We need a tracker to keep track of position in linked list 
```cpp
int position = 3;
if (position != 1) {
    Node* current = head;
    for (int i = 0; i < position; i++) {
        current = current->next;
    }
}
Node* temp = new Node(12);
temp->next = current->next;
current->next = temp;
if (temp->next == nullptr) {
    // newly added node is the last one
    tail = temp;
} else {
    // adding to head
    Node* temp = new Node(12);
    temp->next = head;
    head = temp;
}
```

### Destructor
Run through the list, pointing to head and next, deleting head each time, updating the new head to next, till you haven't reached the end of the loop (nullptr)

```cpp
while (head) {
    .....
}
```

**Node Sequences** are
- Slower to retrieve elements in sequence
- Faster to add element in middle of sequence
- Can grow dynamically, no need to resize

## Dynamic Structures
- Dynamic: dynamic memory allocation is used in some way
- Structures: use pointers to other data in some way to create data structures
- **Singly Linked Lists**: head, tail, next
- **Doubly Linked Lists**: head, tail, prev, next
- **Simple binary tree**: root, left, right 