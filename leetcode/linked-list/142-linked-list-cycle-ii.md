# 142-linked-list-cycle-ii

## Question {#question}

[https://leetcode.com/problems/linked-list-cycle-ii/description/](https://leetcode.com/problems/linked-list-cycle-ii/description/)

Given a linked list, return the node where the cycle begins. If there is no cycle, return`null`.

**Note:**Do not modify the linked list.

**Follow up**:  
Can you solve it without using extra space?

**Example:**

```text

```

## Thought Process {#thought-process}

1. Hash Table
   1. Use hash table to record the node visited
   2. Time complexity O\(n\)
   3. Space complexity O\(n\)
2. Floyd's Tortoise and Hare
   1. Let's say that F is the length of noncyclic part, and C is the length of cycle
   2. Check article here, [https://leetcode.com/articles/linked-list-cycle-ii/](https://leetcode.com/articles/linked-list-cycle-ii/)
   3. When tortoise reach the start of cycle, index 0, hare has traveled 2F step at F mod C index, call it index h
   4. If we move tortoise C - h steps, hare moves 2 \(C - h\) moves, they reach at the same index
   5. h + 2 \(C - h\) = 2C - h, taking the mod again, \(2C - h\) mod C = C - h
   6. Then we reinitialize one of the pointer back to the start of the list, move both pointers at the pace of 1
   7. They will collide at the start of cycle, let's say they meet at point a, index a in the loop
   8. 2 \* distance\(tortoise\) = distance\(hare\)
   9. 2F + 2a = F + a + b + a + nC, where n &gt;= 0
   10. F = nC + b, since a + b = C, moving from a F steps and moving from 0 F steps, the pointers collide at the entrance of cycle
   11. Time complexity O\(n\)
   12. Space complexity O\(1\)

## Solution

```java
public class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode slow = head, fast = head;
        do {
            if (fast == null || fast.next == null) return null;
            slow = slow.next;
            fast = fast.next.next;
        } while (slow != fast);
        fast = head;
        while (fast != slow){
            fast = fast.next;
            slow = slow.next;
        }
        return slow;
    }
}
```

## Additional {#additional}

