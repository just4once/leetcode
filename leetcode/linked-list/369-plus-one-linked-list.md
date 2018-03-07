### Question {#question}

[https://leetcode.com/problems/plus-one-linked-list/description/](https://leetcode.com/problems/plus-one-linked-list/description/)

Given a non-negative integer represented as **non-empty**a singly linked list of digits, plus one to the integer.

You may assume the integer do not contain any leading zero, except the number 0 itself.

The digits are stored such that the most significant digit is at the head of the list.

**Example:**

```
Input:
1->2->3

Output:
1->2->4
```

### Thought Process {#thought-process}

1. To List and Back
   1. Time complexity O\(n\)
   2. Space complexity O\(n\)
2. Prepend node
   1. Add a dummy node in the front
   2. Time complexity O\(n\)
   3. Space complexity O\(1\)

### Solution

```java
class Solution {
    public ListNode plusOne(ListNode head) {
        List<Integer> nums = new ArrayList<>();
        ListNode cur = head;
        while (cur != null) {
            nums.add(cur.val);
            cur = cur.next;
        }
        boolean carry = false;
        for (int i = nums.size() - 1; i >= 0; i--) {
            if (nums.get(i) < 9) {
                nums.set(i, nums.get(i) + 1);
                carry = false;
                break;
            } else {
                nums.set(i, 0);
                carry = true;
            }
        }
        ListNode dummy = new ListNode(-1);
        if (carry) {
            dummy.next = new ListNode(1);
            dummy.next.next = head;
        } else {
            dummy.next = head;
        }
        for (int num : nums) {
            head.val = num;
            head = head.next;
        }
        return dummy.next;
    }
}
```

```java
class Solution {
    public ListNode plusOne(ListNode head) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode beforeNine = dummy, lastNode = dummy;
        while (lastNode.next != null) {
            lastNode = lastNode.next;
            if (lastNode.val != 9) {
                beforeNine = lastNode;
            }
        }
        beforeNine.val++;
        while (beforeNine.next != null) {
            beforeNine = beforeNine.next;
            beforeNine.val = 0;
        }
        return dummy.val == 0 ? dummy.next : dummy;
    }
}
```

### Additional {#additional}



