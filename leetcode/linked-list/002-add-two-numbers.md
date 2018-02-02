### Question {#question}

[https://leetcode.com/problems/add-two-numbers/description/](https://leetcode.com/problems/add-two-numbers/description/)

You are given two **non-empty **linked lists representing two non-negative integers. The digits are stored in **reverse order **and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example:**

```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```

### Thought Process {#thought-process}

1. Since the digits are stored in reverse order, the solution is pretty straight forward. The only thing we need to be careful about is the possibility of carry over.
2. Dummy node is helpful to return the head of the linked list \(the "last" digit of the number\).
3. Time complexity is O\(n\)
4. Space complexity is O\(n\) for creating new linked list or O\(1\) for reusing one of the input

### Solution {#solution}

```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(-1);
        ListNode cur = dummy;
        int sum = 0;
        while(l1!=null || l2!=null){
            sum /= 10;
            if(l1!=null){
                sum+=l1.val;
                l1 = l1.next;
            }
            if(l2!=null){
                sum+=l2.val;
                l2 = l2.next;
            }
            cur.next = new ListNode(sum%10);
            cur = cur.next;
        }
        if(sum >= 10){
            cur.next = new ListNode(1);
        }
        return dummy.next;
    }
}
```

### Additional {#additional}



