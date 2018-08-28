# 082-remove-duplicates-from-sorted-list-ii

## Question {#question}

[https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/description/](https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/description/)

Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.

**Example:**

```text
Given 1->2->3->3->4->4->5, return 1->2->5.
Given 1->1->1->2->3, return 2->3.
```

## Thought Process {#thought-process}

1. Compare Next Node
   1. Simply compare every node to its next node, move the pointers forward if the cur node's value is same as next
   2. If the previous node's next node is still same as current, we haven't move the pointer forward, which means the node has no duplicate
   3. Time complexity O\(n\)
   4. Space complexity O\(1\)

## Solution

```java
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode pre = dummy, cur = head;
        while(cur != null){
            while (cur.next != null && cur.next.val == cur.val) {
                cur = cur.next;
            }
            if (pre.next == cur) pre = pre.next;
            else pre.next = cur.next;
            cur = cur.next;
        }
        return dummy.next;
    }
}
```

## Additional {#additional}

