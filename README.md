# 100-days-of-Code
Keeping myself honest. Talk is cheap.

No work days = 3

## Day 16 - 12 Mar 2020 [6:42 am, hopefully more programming today]
1-  Implement two stacks in one array. 

Support these operations:

push1() // to push in the first stack

push2() // to push in the second stack

pop1()

pop2()

isEmpty1()

isEmpty2()

isFull1()

isFull2()

Make sure your implementation is space efficient. (hint: do not allocate the same amount of space by dividing the array in half.) 

```Java 
// WORK IN PROGRESS
public class TwoStacks {
    int[] stack = new int[10];
    int count1 = 0;
    int count2 = 0;

    public void push1(int element) {
        if (count1 + count2 == 10) {
            throw new StackOverflowError("Stack is full");
        }
        else if (count1 + count2 == 0) {
            stack[0] = element;
            count1++;
        }
        else {
            // Shift the array
            int[] secondStack = Arrays.copyOfRange(stack, count1, count1 + count2);
            stack[count1] = element;
            count1++;
            for (int i = 0; i < count2; i++) {
                stack[count1 + i] = secondStack[i];
            }
        }
    }

    public void push2(int element) {
        if (count1 + count2 == 10) {
            throw new StackOverflowError("Stack is full");
        }
        else if (count1 + count2 == 0) {
            stack[0] = element;
            count2++;
        }
        else {
            stack[count1 + count2] = element;
            count2++;
        }
    }

    public void printStack() {
        for (int i = 0; i < stack.length; i++) {
            System.out.println(stack[i]);
        }
    }

}
```


## Day 15 - 11 Mar 2020
Read about GraphQL and difference between GraphQL and REST. https://medium.com/@back4apps/graphql-vs-rest-62a3d6c2021d  

Continued working through the Algorithms & DS course. Wrote a stack implementation using an array. 
```Java
@SuppressWarnings("SpellCheckingInspection")
public class Stack {
    private int[] stack = new int[5];
    private int count = 0;

    public void push(int element) {
        if (count < stack.length) {
            stack[count] = element;
        }
        else {
            // We need to create a new array
            int[] newArray = new int[stack.length + 1];
            // TODO: Refactor into an arrayCopy function
            for (int i = 0; i < stack.length; i++) {
               newArray[i] = stack[i];
            }
            newArray[stack.length] = element;
            stack = newArray;
        }
        count++;
    }

    public int pop() {
        return stack[count - 1];
    }



    // Old inefficient implementation
    // public void push(int element) {
    //
    //     if (element == 0) {
    //         throw new IllegalArgumentException("Cannot push 0 to stack");
    //     }
    //     Boolean itemAdded = false;
    //     // Couldn’t remember how to check the size of an array! length() or size(). It’s length.
    //     for (int i = 0; i < stack.length; i++) {
    //         if (stack[i] == 0) {
    //             stack[i] = element;
    //             itemAdded = true;
    //             break;
    //         }
    //     }
    //     if (itemAdded == false) {
    //         // We need to create a new array
    //         int[] newArray = new int[stack.length + 1];
    //         // TODO: Refactor into an arrayCopy function
    //         for (int i = 0; i < stack.length; i++) {
    //            newArray[i] = stack[i];
    //         }
    //         newArray[stack.length] = element;
    //         stack = newArray;
    //     }
    // }
    //
    // public int pop() {
    //     int last_index = stack.length - 1;
    //     // Partially filled "stack
    //     if (stack[last_index] != 0) {
    //         return stack[last_index];
    //     } else {
    //         int i = last_index;
    //         while (i > 0) {
    //             if (stack[i] == 0)
    //                 i--;
    //             else
    //                 break;
    //         }
    //         return stack[i];
    //     }
    // }

    public void printStack() {
        for (int i = 0; i < stack.length; i++) {
            System.out.println(stack[i]);
        }
    }
}


```


## Day 14 - 10 March 2020
I tried to write another simple (but common) stack problem. Checking if an expression is valid. While this isn't by any means a complete check, but I am happy I was able to write it 75% accurately on Google Docs and the algoritm was correct in the first try. This implementation is a much cleaner than my earlier implementation of this. 
```Java
import java.util.Stack;

public class ExpressionChecker {
    /**
     * Given an expression like [(1 + 2) * 3 + (9 - 8)] or )()(
     * this function tells whether it is a valid expression or not.
     * First one is valid, second one isn't.
     */

    public boolean isValid(String input) {
        Stack<Character> S = new Stack<>();
        Boolean cont = true;
        for (Character c : input.toCharArray()) {
            if (cont) {
                switch (c) {
                    case '(':
                    case '{':
                    case '[':
                        S.push(c);
                        break;
                    case ')':
                        if (!S.isEmpty()) {
                            if (S.pop() != '(') {
                                cont = false;
                            }
                        } else {
                            S.push(c);
                            cont = false;
                        }
                        break;
                    case '}':
                        if (!S.empty()) {
                            if (S.pop() != '{') {
                                cont = false;
                            }
                        } else {
                            cont = false;
                        }
                        break;
                    case ']':
                        if (!S.empty()) {
                            if (S.pop() != '[') {
                                cont = false;
                            }
                        } else {
                            cont = false;
                        }
                        break;
                    default:
                        break;
                }
            }
        }
        if (S.isEmpty()) {
            return true;
        } else {
            return false;
        }
    }
}
```

## Day 13 - 9 March 2020
I learned the difference between StringBuffer and String in the process of writing a "Hello Stacks" class. Using a StringBuffer is more efficient than using a String because in Java an object of class String is immutable. So every append is essentially like creating a new String object. 

https://javarevisited.blogspot.com/2011/07/string-vs-stringbuffer-vs-stringbuilder.html


```Java
import java.util.Stack;

public class StringReverser {
    public String reverse(String input) {
        Stack<Character> stack = new Stack<>();
        for (Character ch: input.toCharArray()) {
            stack.push(ch);
        }

        StringBuffer reversed = new StringBuffer();
        while (!stack.isEmpty()){
            reversed.append(stack.pop());
        }

        return reversed.toString();
    }
}
```



## Day 12 - 8 March 2020
Wrote a function to check if a LinkedList has a loop. This is using the tortoise/hare technique. A moves to the next element where B moves to the next to the next element. When they meet (A == B), you return true. If there is no loop, there will be a NullPointerException and we return false. 

```Java
public boolean hasLoop() {
    if (head == null || head == tail)
        return false;
    else {
        try {
            var A = head;
            var B = head;
            while (A != null) {
                A = A.next;
                B = B.next.next;

                if (A == B)
                    return true;
            }
            return false;
        }
        catch(NullPointerException ex) {
            return false;
        }

    }
}
```

## [NO WORK] Day 11 - 7 March 2020
Busy Saturday with the family

## Day 10 - 6 March 2020
I took hints and felt really $#!tty about it. The goal of this relearning is to learn **how to solve** and not to find out the solution to a particular problem. So to make myself feel a little less $#!tty, I didn't absolutely look at the code and coded it on a piece of paper. Then I wrote the code in IntelliJ and with the exception on on small edge case testing, it was flawless. 
```Java
// We don't know if the list has an even or odd number of elements
public void printMiddle() {
    if (head == null)
        System.out.println(-1);
    else if (head == tail)
        System.out.println(head.value);
    else {
        int nodeCount = 0;
        var current = head;
        var midPoint = current;
        while (current != null) {
            for (int i = 0; i < 2; i++) {
                if (current != null) {
                    current = current.next;
                    nodeCount++;
                    // MISTAKE was here. We don't need to increment the midPoint if nodeCount is 1
                    if (nodeCount > 1 && nodeCount % 2 != 0) {
                        midPoint = midPoint.next;
                    }
                }
            }
        }
        System.out.println(midPoint.value);
        if (nodeCount % 2 == 0) {
            // Even number of elements
            System.out.println(midPoint.next.value);
        }
    }
}
```

## [NO WORK] Day 9 - 5 March 2020
I had to take hints on the problem from Day 8. Tried a little bit. But couldn't finish it. 

## Day 8 - 4 March 2020
How can you find the middle element of a **singly** linked list in a **single pass**? 

**Sol 1** Loop through the list and keep adding elements to an ArrayList. Read the middle element in O(1) time.
Time complexity: O(n), Space complexity: Poor, as we are creating a new data structure

**Sol 2** Use the getKthNodeFromTheEnd method (Day 6), keep incrementing k until head == tail. But for even number of elements, this won't work as the head and tail will not meet. And **it is not single pass**.

Will think a bit more on this. 


## [NO WORK] Day 7 - 3 March 2020
Sick kid and traveling wife. 

## Day 6 - 2 March 2020
Hectic day at work and then family time. 

1) Read about "Illusion of Competence". How you can study something and not forget. Create (good) vs. Understand (bad)

2) Got the getKthNodeFromTheEnd implementation modified without using the size class vairbale. 
```java
public int getKthNodeFromTheEnd(int k) throws Exception {
    if (k > 0) {
        var firstPointer = head;
        var nextPointer = head;
        for (int i = 0; i < k - 1; i++) {
            nextPointer = nextPointer.next;
            if (nextPointer == null) {
                throw new IllegalArgumentException("k is too big");
            }
        }
        while (nextPointer.next != null) {
            firstPointer = firstPointer.next;
            nextPointer = nextPointer.next;
        }
        return firstPointer.value;
    } else throw new IllegalArgumentException("k must be greater than 0");
 }
```

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
    tail = head;
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
