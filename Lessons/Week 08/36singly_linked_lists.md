# 03/10/2022: Singly Linked Lists

## Implement Singly Linked Lists

**SinglyLinkedList header file**
```cpp
class SinglyLinkedList {
public:
    SinglyLinkedList();
    ~SinglyLinkedList();
    void PushBack(int value);
private:
    // note these lay on stack
    // these POINT TO items in free store
    Node* head_;
    Node* tail_;
};
```

**SinglyLinkedList c++ file**
```cpp
SinglyLinkedList::SinglyLinkedList() : head_(nullptr), tail_(nullptr) {
    // initialized
}

SinglyLinkedList::PushBack(int value) {
    // CASE 1: list is length 0
    if (head_ == nullptr) {
        head_ = tail_ = new Node(value);
    }
    // CASE 2: list contains elements already
    else {
        Node* new_node = new Node(value);
        tail_->next = new_node;
        tail_ = new_node;
        // new_node will be popped off the stack
    }
}

SinglyLinkedList::~SinglyLinkedList() {
    while(head_) {
        Node* next = head->next;
        delete head_;
        head_ = next;
    }
    // node: tail is not considered dangling pointer at the end of destruction
}
```

## Traversing Linked List
Do not use head to traverse linked list because we have now lost all references to this list. We can never get back to where we came from. Loss of head = memory leak since we cannot call delete on it 

```cpp
// craft conditional based on where you need to get to

while (end of the linked list) {
    current = current->next
}

while (where you need to get to) {
    current = current->next;
}
```