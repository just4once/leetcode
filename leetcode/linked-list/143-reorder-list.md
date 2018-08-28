# 143-reorder-list

## Question {#question}

[https://leetcode.com/problems/reorder-list/description/](https://leetcode.com/problems/reorder-list/description/)

Given a singly linked listL:L0→L1→…→Ln-1→Ln,  
reorder it to:L0→Ln→L1→Ln-1→L2→Ln-2→…

You must do this in-place without altering the nodes' values.

**Example:**

```text
Given {1,2,3,4}, reorder it to {1,4,2,3}.
```

## Thought Process {#thought-process}

1. Reverse and Link
   1. Reverse the second half of linked list and then relink
   2. Time complexity O\(n\)
   3. Space complexity O\(1\)

## Solution

```java
class Solution {
    public void reorderList(ListNode head) {
        if (head == null || head.next == null) return;
        ListNode slow = head, fast = head;
        while (fast.next != null && fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        // split the list into two equal parts, left has one extra
        // element when the length is odd
        ListNode rightHead = reverse(slow.next);
        slow.next = null;
        ListNode left = head, right = rightHead;
        while (right != null) {
            ListNode nLeft = left.next;
            left.next = right;
            right = right.next;
            left.next.next = nLeft;
            left = nLeft;
        }
    }

    private ListNode reverse(ListNode head) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode pre = dummy, cur = head;
        while (cur.next != null) {
            ListNode newHead = cur.next;
            cur.next = newHead.next;
            newHead.next = pre.next;
            pre.next = newHead;
        }
        return dummy.next;
    }
}
```

## Additional {#additional}

