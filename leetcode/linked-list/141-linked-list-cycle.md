# 141-linked-list-cycle

## Question {#question}

[https://leetcode.com/problems/linked-list-cycle/description/](https://leetcode.com/problems/linked-list-cycle/description/)

Given a linked list, determine if it has a cycle in it.

Follow up:

Can you solve it without using extra space?

**Example:**

```text

```

## Thought Process {#thought-process}

1. Hash Table
   1. Use hash table to record the node visited
   2. Time complexity O\(n\)
   3. Space complexity O\(n\)
2. Two Pointer
   1. Classic Tortoise and Hare Algorithm or Floyd's Cycle detection algorithm
   2. Slow pointer move at the pace of 1 and fast pointer moves at the pace of 2
   3. Fast pointer is the one who catch up with slow
   4. If slow and fast meet, we know there is cycle
   5. Time complexity O\(n\)
   6. Space complexity O\(1\)

## Solution

```java
public class Solution {
    public boolean hasCycle(ListNode head) {
        ListNode slow = head, fast = head;
        while (fast!= null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) return true;
        }
        return false;
    }
}
```

## Additional {#additional}

