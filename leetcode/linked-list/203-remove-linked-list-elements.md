### Question {#question}

[https://leetcode.com/problems/remove-linked-list-elements/description/](https://leetcode.com/problems/remove-linked-list-elements/description/)

Remove all elements from a linked list of integers that have value **val**.

**Example:**

```
Given: 1 --> 2 --> 6 --> 3 --> 4 --> 5 --> 6, val = 6
Return: 1 --> 2 --> 3 --> 4 --> 5
```

### Thought Process {#thought-process}

1. Iterative
   1. Time complexity O\(n\)
   2. Space complexity O\(1\)
2. Recursion
   1. Time complexity O\(n\)
   2. Space complexity O\(1\)

### Solution

```java
class Solution {
    public ListNode removeElements(ListNode head, int val) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode pre = dummy;
        while (pre.next != null){
            if (pre.next.val == val){
                pre.next = pre.next.next;
            } else {
                pre = pre.next;
            }
        }
        return dummy.next;
    }
}
```

```java
class Solution {
    public ListNode removeElements(ListNode head, int val) {
        if (head == null) return null;
        head.next = removeElements(head.next, val);
        return head.val == val ? head.next : head;
    }
}
```

### Additional {#additional}



