### Question {#question}

[https://leetcode.com/problems/insertion-sort-list/description/](https://leetcode.com/problems/insertion-sort-list/description/)

Sort a linked list using insertion sort.

**Example:**

```

```

### Thought Process {#thought-process}

1. Pointer
   1. Use dummy variable to point to head and a another variable track the progress the variable
   2. We need to find the node that the current node is greater than its next node, and that's where we insert the current node
   3. Time complexity O\(n^2\)
   4. Space complexity O\(1\)

### Solution

```java
class Solution {
    public ListNode insertionSortList(ListNode head) {
        ListNode dummy = new ListNode(Integer.MIN_VALUE);
        ListNode pre = dummy;
        while (head != null) {
            ListNode next = head.next;
            if (head.val < pre.val) pre = dummy;
            while (pre.next != null && head.val > pre.next.val) pre = pre.next;
            head.next = pre.next;
            pre.next = head;
            head = next;
        }
        return dummy.next;
    }
}
```

### Additional {#additional}



