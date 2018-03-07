### Question {#question}

[https://leetcode.com/problems/palindrome-linked-list/description/](https://leetcode.com/problems/palindrome-linked-list/description/)

Given a singly linked list, determine if it is a palindrome.

**Follow up:**  
Could you do it in O\(n\) time and O\(1\) space?

**Example:**

```

```

### Thought Process {#thought-process}

1. Reversed
   1. By reversing the second half of the list, we can compare the list node by node
   2. Time complexity O\(n\)
   3. Space complexity O\(1\)

### Solution

```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode l1r = reverse(l1), l2r = reverse(l2);
        ListNode cur = new ListNode(0);
        int sum = 0;
        while (l1r != null || l2r != null) {
            if (l1r != null) {
                sum += l1r.val;
                l1r = l1r.next;
            }
            if (l2r != null) {
                sum += l2r.val;
                l2r = l2r.next;
            }
            cur.val = sum % 10;
            sum /= 10;
            ListNode head = new ListNode(sum);
            head.next = cur;
            cur = head;
        }
        return cur.val == 0 ? cur.next : cur;
    }
    
    private ListNode reverse(ListNode node) {
        ListNode dummy = new ListNode(-1), next;
        while (node != null) {
            next = node.next;
            node.next = dummy.next;
            dummy.next = node;
            node = next;
        }
        return dummy.next;
    }
}
```

```java
class Solution {
    public boolean isPalindrome(ListNode head) {
        if (head == null || head.next == null) return true;
        ListNode slow = head, fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        ListNode reversed = reverse(slow);
        while (head != slow && head.val == reversed.val) {
            head = head.next;
            reversed = reversed.next;
        }
        return head == slow;
    }

    public ListNode reverse(ListNode node) {
        ListNode dummy = new ListNode(-1), next;
        while (node != null) {
            next = node.next;
            node.next = dummy.next;
            dummy.next = node;
            node = next;
        }
        return dummy.next;
    }
}
```

### Additional {#additional}



