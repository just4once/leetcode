### Question {#question}

You are given two **non-empty **linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Follow up:**  
What if you cannot modify the input lists? In other words, reversing the lists is not allowed.

**Example:**

```
Input: (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 8 -> 0 -> 7
```

### Thought Process {#thought-process}

1. Reverse and Add
   1. Time complexity O\(n\)
   2. Space complexity O\(1\)
2. Stack
   1. By adding the val to the stack, we get the values in reverse, which means we create the tail first and then adding the head one by one
   2. Time complexity O\(n\)
   3. Space complexity O\(n\)

### Solution

```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        Stack<Integer> stack1 = getVal(l1);
        Stack<Integer> stack2 = getVal(l2);
        ListNode cur = new ListNode(0);
        int sum = 0;
        while (!stack1.isEmpty() || !stack2.isEmpty()) {
            if (!stack1.isEmpty()) sum += stack1.pop();
            if (!stack2.isEmpty()) sum += stack2.pop();
            cur.val = sum % 10;
            sum /= 10; //carry
            ListNode head = new ListNode(sum);
            head.next = cur;
            cur = head;
        }
        return cur.val == 0 ? cur.next : cur;
    }
    
    private Stack<Integer> getVal(ListNode l) {
        Stack<Integer> stack = new Stack<>();
        while (l != null) {
            stack.push(l.val);
            l = l.next;
        }
        return stack;
    }
}
```

### Additional {#additional}



