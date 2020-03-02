# 100-days-of-Code
Keeping myself honest. Talk is cheap. 

## Day 5 - 1 March 2020
Get k-th node from the end of a singly linked list. Need to write a solution which is unaware of the size of the linked list.
```java
public int getKthNodeFromTheEnd(int k) throws Exception {
    if (k > 0) {
        if (k <= size) {
            var firstPointer = head;
            var nextPointer = head;
            for (int i = 0; i < k - 1; i++) {
                nextPointer = nextPointer.next;
            }
            while (nextPointer.next != null) {
                firstPointer = firstPointer.next;
                nextPointer = nextPointer.next;
            }
            return firstPointer.value;
        } else throw new Exception("K can't be greater than " + size + ", the size of the list.");
    } else throw new Exception("Invalid parameter. Enter a value between 1 and " + size + ".");
 }
```

## Day 4 - 29 Feb 2020
Finally figured out how to reverse a LinkedList in place. Took me a crazy amount of time but it was time well spent. I started working on it Friday afternoon, then worked Saturday from 5am to about 6:30 am. Then finally finished it when working Sunday (March 1st) between 4am and 5:30am. I am sure this can be made a lot leaner. I don't like the part where I check if prev == head and then set prev.next to null. This was hacky and put in place make sure the first node is no longer the head.

```Java
public void reverse() {
    var current = head;
    var prev = head;
    while (current != null) {
        var next = current.next;
        current.next = prev;
        // Ensure the last node in the reversed list doesn't point to anything.
        if (prev == head) {
            prev.next = null;
        }
        prev = current;
        current = next;
        // Stop head from moving beyond the tail
        if (next != null) {
            head = next;
        }
    }
 }
 ```

## Day 3 - 28 Feb 2020
- Stuck with reversing a LinkedList in place.

## Day 2 - 27 Feb 2020
- My own Java implementation of the LinkedList class. Write functions likes addFirst, addLast, deleteFirst, deleteLast, delete and indexOf

## Day 1 - 26 Feb 2020
- Read the dynamic programming PDF by Sam Gavis-Hughson (Byte-by-Byte) - the introduction and motivation part.
