### Question {#question}

Reverse a linked list from position m to n. Do it in-place and in one-pass.

**Example:**

```
Given 1->2->3->4->5->NULL, m = 2 and n = 4,

return 1->4->3->2->5->NULL.
```

### Thought Process {#thought-process}

1. Move Pointer
   1. Move pointer to the mth position, then reverse
   2. Time complexity O\(n\)
   3. Space complexity O\(1\)

### Solution

```java
class Solution {
    public ListNode reverseBetween(ListNode head, int m, int n) {
        if (head == null || m == n) return head;
        int len = n - m;
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode pre = dummy;
        while(m > 1){
            pre = pre.next;
            m--;
        }
        ListNode cur = pre.next, remain = cur.next;
        while(len-- > 0){
            cur.next = remain.next;
            remain.next = pre.next;
            pre.next = remain;
            remain = cur.next;
        }
        return dummy.next;
    }
}
```

### Additional {#additional}



