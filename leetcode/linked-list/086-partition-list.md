# 086-partition-list

## Question {#question}

[https://leetcode.com/problems/partition-list/description/](https://leetcode.com/problems/partition-list/description/)

Given a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.

**Example:**

```text
Given 1->4->3->2->5->2 and x = 3,
return 1->2->2->4->3->5.
```

## Thought Process {#thought-process}

1. Two Pointers
   1. Save the vale into different pointers
   2. Link the two pointers at the end
   3. Time complexity O\(n\)
   4. Space complexity O\(1\)

## Solution

```java
class Solution {
    public ListNode partition(ListNode head, int x) {
        ListNode less = new ListNode(-1), greater = new ListNode(0);
        ListNode dummyLess = less, dummyGreater = greater;
        while (head != null){
            if (head.val < x){
                less.next = head;
                less = head;
            } else {
                greater.next = head;
                greater = head;
            }
            head = head.next;
        }
        greater.next = null;
        less.next = dummyGreater.next;
        return dummyLess.next;
    }
}
```

## Additional {#additional}

