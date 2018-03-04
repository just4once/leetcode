### Question {#question}

Given a sorted linked list, delete all duplicates such that each element appear only once.

**Example:**

```
Given 1->1->2, return 1->2.
Given 1->1->2->3->3, return 1->2->3.
```

### Thought Process {#thought-process}

1. Compare next node
   1. Link the cur node to next.next if same as current
   2. Time complexity O\(n\)
   3. Space complexity O\(1\)

### Solution

```java
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        ListNode cur = head;
        while(cur != null && cur.next != null){
            if(cur.val == cur.next.val) cur.next = cur.next.next;
            else cur = cur.next;
        }
        return head;
    }
}
```

### Additional {#additional}



