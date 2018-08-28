# 019-remove-nth-node-from-end-of-list

## Question {#question}

[https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/](https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/)

Given a linked list, remove the nth node from the end of list and return its head.

**Example:**

```text
Given linked list: 1->2->3->4->5, and n = 2.

After removing the second node from the end, the linked list becomes 1->2->3->5.
```

## Thought Process {#thought-process}

1. Two Passes
   1. Count the length and then we know where to remove the element
   2. Time complexity O\(n\)
   3. Space complexity O\(1\)
2. One Pass
   1. Use two pointers to track the position
   2. We move one pointer n position forward, and the other at the start
   3. Then we move both pointers at the same pace, when the first pointer reach the end, the other pointer is at the positon before the removing node
   4. Time complexity O\(n\)
   5. Space complexity O\(1\)

## Solution

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        ListNode cur = head;
        int size = 0;
        while(cur != null){
            size++;
            cur = cur.next;
        }
        size -= n;
        cur = dummy;
        while(size > 0){
            size--;
            cur = cur.next;
        }
        cur.next = cur.next.next;
        return dummy.next;
    }
}
```

```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        ListNode first = dummy, second = dummy;
        for (int i = 0; i <= n; i++) first = first.next;
        while (first != null) {
            first = first.next;
            second = second.next;
        }
        second.next = second.next.next;
        return dummy.next;
    }
}
```

## Additional {#additional}

