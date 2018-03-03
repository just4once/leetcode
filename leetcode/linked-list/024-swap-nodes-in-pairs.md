### Question {#question}

Given a linked list, swap every two adjacent nodes and return its head.

**Example:**

```
Given 1->2->3->4, you should return the list as 2->1->4->3.
```

Your algorithm should use only constant space. You may not modify the values in the list, only nodes itself can be changed.

### Thought Process {#thought-process}

1. Iterative
   1. Make sure we have next two nodes available to swap the position
   2. Time complexity O\(n\)
   3. Space complexity O\(1\)
2. Recursion
   1. Time complexity O\(n\)
   2. Space complexity O\(n\) for recursion stack

### Solution

```java
class Solution {
    public ListNode swapPairs(ListNode head) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode cur = dummy;
        while (cur.next != null && cur.next.next != null) {
            ListNode next = cur.next;
            cur.next = next.next;
            next.next = cur.next.next;
            cur.next.next = next;
            cur = next;
        }
        return dummy.next;
    }
}
```

```java
class Solution {
    public ListNode swapPairs(ListNode head) {
        if (head == null || head.next == null) return head;
        ListNode newHead = head.next;
        head.next = swapPairs(newHead.next);
        newHead.next = head;
        return newHead;
    }
}
```

### Additional {#additional}



