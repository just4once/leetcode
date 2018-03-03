### Question {#question}

Given a linked list, reverse the nodes of a linked list k at a time and return its modified list.

k is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of k then left-out nodes in the end should remain as it is.

You may not alter the values in the nodes, only nodes itself may be changed.

Only constant memory is allowed.

**Example:**

```
Given this linked list: 1->2->3->4->5

For k = 2, you should return: 2->1->4->3->5

For k = 3, you should return: 3->2->1->4->5
```

### Thought Process {#thought-process}

1. Iterative
   1. Reverse the node in the range
   2. If we don't have enough node, we stop
   3. Time complexity O\(n\)
   4. Space complexity O\(1\)
2. Recursion
   1. Time complexity O\(n\)
   2. Space complexity O\(n/k\) due to recursion stack

### Solution

```java
class Solution {
    public ListNode reverseKGroup(ListNode head, int k) {
        if(k == 1) return head;
        ListNode dummy = new ListNode(0), pre = dummy;
        dummy.next = head;
        ListNode last = kthNode(pre, k);
        while (last != null) {
            // reset the pre to the tail of range
            pre = reverseNextK(pre, k);
            last = kthNode(pre, k);
        }
        return dummy.next;
    }
    
    private ListNode kthNode(ListNode head, int k) {
        while (head != null && k > 0) {
            head = head.next;
            k--;
        }
        return head;
    }
    
    private ListNode reverseNextK(ListNode pre, int k) {
        ListNode head = pre.next;
        while (--k > 0) {
            ListNode newHead = head.next;
            head.next = newHead.next;
            newHead.next = pre.next;
            pre.next = newHead;
        }
        return head;
    }
}
```

```java
class Solution {
    public ListNode reverseKGroup(ListNode head, int k) {
        ListNode cur = head;
        int n = 0;
        // move the cur to start of next range
        while (cur != null && n < k) {
            cur = cur.next;
            n++;
        }
        // we have enough nodes
        if (n == k) {
            cur = reverseKGroup(cur, k);
            while (n-- > 0) {
                ListNode newHead = head.next;
                head.next = cur;
                cur = head;
                head = newHead;
            }
            head = cur;
        }
        return head;
    }
}
```

### Additional {#additional}



