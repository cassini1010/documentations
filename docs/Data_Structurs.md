# Data Structures

## Linked List

Since adding and deleting of the element at the beginning and end of a list is efficient using `linked lists` , these are used to construct `Queues`

| Operation                           | Time Complexity of List | Time Complexity of Linked List |                                                                 |
| ----------------------------------- | ----------------------- | ------------------------------ | --------------------------------------------------------------- |
| add/remove element to the beginning | O(n)                    | O(1)                           |                                                                 |
| add/remove element at the end       | O(1)                    | O(1)                           |                                                                 |
| Retrieve element                     | O(1)                    | O(n)                           | List uses indexes which is faster. Linked list uses traversing. |
| Search for specific element         | O(n)                    | O(n)                           | Both uses traversing to search element                          |

`List` uses contiguous memory allotment. To append to the left/head of the list it takes O(n) computations, as a new empty memory block has to be created at the beginning of the list. This operation requires existing elements to shift one position to the right resulting in `n` operations. Similarly, removing an element form the left also requires each remaining elements to be shifted to the left, resulting in `n-1` operations and hence O(n) time complexity.

On the other hand append and pop form the right doesn't need shifting of `n` elements from the  list. hence O(1) time complexity.

## collections.deque (pronounced `deck`)

This is the `linked list` implementation in python. Takes `O(1)` time complexity. Easy to insert, remove, access element from both ends of a list.

Recommended to be used for the implementation of `queues` and `stacks`

If thread operations are used on  `queues` and `stacks` , it is recommended to use `Queues` library in python. But `deques` can also be used with some trade offs. 

<mark>`deques` have a feature to restrict the maximum length of your deques.</mark>





## Linked list without using `deque` library:

`SinglyLinkedList` has `head` as a parameter. The efficiency can be increased a little by adding a `tail` parameter. Although `tail` parameter do not help in pop() method, it at least helps in other operations.

```python
SinglyLinkedList.py


class EmptyLinkedList(Exception):
    ...

class Node:
    def __init__(self, data:str) -> None:
        self.data = str(data)
        self.next = None

class SingleLinkedList:
    def __init__(self) -> None:
        self.head = None
        self.tail = None
    
    def __repr__(self) -> str:
        head = self.head
        sll_repr = []
        while head:
            sll_repr.append(head.data)
            head = head.next
        return "->".join(sll_repr)
    
    def append(self, data):
        '''- This method doesn't use the tail parameter
           - Uses traversal to get to the point where append
             needs to be done.
           - Traversal takes time for larger list O(n)'''
        head = self.head
        if head == None:
            head = Node(data)
            self.head = head
            return None
        while head.next:
            head = head.next
        head.next = Node(data)

    def pop(self):
        '''- This method doesn't use the tail parameter
           - Uses traversal to get to the point where remove
             needs to be done.
           - Traversal takes time for larger list O(n)'''
        head = self.head
        if head == None:
            raise EmptyLinkedList("Operating on empty linked list")
        elif head.next == None:
            self.head = None
            return None
        while head.next.next:
            head = head.next
        head.next = None

    def tail_pop(self):
        '''pop using tail parameter is not possible in singly linked list
            Because tail is pointing to last element which is supposed to be removed
            pointing it to the one element previous to tail needs another pointer
        '''

    def append_left(self, data):
        '''append_left also takes O(1) as head pointer is always pointing to 
        the beginning of the list'''
        head = self.head
        new_node = Node(data)
        new_node.next = head
        self.head = new_node

    def pop_left(self):
        '''pop left takes O(1) as head pointer is already there'''
        try:
            self.head = self.head.next
        except AttributeError:
            raise EmptyLinkedList("Operating on empty linked list") from None
        
    def tail_append(self, data):
        '''- Tail append uses tail parameter
           - appending to the tail takes O(1) time complexity
        '''
        head = self.head
        tail = self.tail
        if head == None:
            head = Node(data)
            self.head, self.tail = head, head
            return None
        if tail == head:
            tail = Node(data)
            self.head.next = tail
            self.tail = tail
            return None
        tail.next = Node(data)
        self.tail = tail.next
```
