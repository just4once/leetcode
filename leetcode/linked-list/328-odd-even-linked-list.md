# 328-odd-even-linked-list

## Question {#question}

[https://leetcode.com/problems/odd-even-linked-list/description/](https://leetcode.com/problems/odd-even-linked-list/description/)

Given a singly linked list, group all odd nodes together followed by the even nodes. Please note here we are talking about the node number and not the value in the nodes.

You should try to do it in place. The program should run in O\(1\) space complexity and O\(nodes\) time complexity.

**Example:**

```text
Given 1->2->3->4->5->NULL,
return 1->3->5->2->4->NULL.
```

**Note:** 

The relative order inside both the even and odd groups should remain as it was in the input.

The first node is considered odd, the second node even and so on ...

## Thought Process {#thought-process}

1. Two pointers
   1. Time complexity O\(n\)
   2. Space complexity O\(1\)

## Solution

```java
class Solution {
    public ListNode oddEvenList(ListNode head) {
        if (head == null) return null;
        ListNode odd = head, even = head.next, evenHead = even;
        while (even != null && even.next != null) {
            odd.next = even.next;
            odd = odd.next;
            even.next = odd.next;
            even = even.next;
        }
        odd.next = evenHead;
        return head;
    }
}
```

## Additional {#additional}

