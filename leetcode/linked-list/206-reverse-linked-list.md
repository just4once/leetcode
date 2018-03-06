### Question {#question}

Reverse a singly linked list.

A linked list can be reversed either iteratively or recursively. Could you implement both?

**Example:**

```

```

### Thought Process {#thought-process}

1. Iterative
   1. Time complexity O\(n\)
   2. Space complexity O\(1\)
2. Recursion
   1. Time complexity O\(n\)
   2. Space complexity O\(1\) or O\(n\) due to recursion stack

### Solution

```java
class Solution {
    public ListNode reverseList(ListNode head) {
        if (head == null) return null;
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode pre = dummy, cur = pre.next, next = null;
        while (cur.next != null) {
            next = cur.next;
            cur.next = next.next;
            next.next = pre.next;
            pre.next = next;
        }
        return dummy.next;
    }
}
```

```
class Solution {
    public ListNode reverseList(ListNode head) {
        return revert(head, null);
    }
    
    private ListNode revert(ListNode head, ListNode tail) {
        if (head == null) return tail;
        ListNode next = head.next;
        head.next = tail;
        return revert(next, head);
    }
}
```

### Additional {#additional}



