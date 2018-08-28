# 148-sort-list

## Question {#question}

[https://leetcode.com/problems/sort-list/description/](https://leetcode.com/problems/sort-list/description/)

Sort a linked list in O\(n log n\) time using constant space complexity.

**Example:**

```text

```

## Thought Process {#thought-process}

1. ArrayList
   1. Save the value to the array list and sort
   2. Update the value accordingly
   3. Time complexity O\(n log n\)
   4. Space complexity O\(n\)
2. Divide and Conquer
   1. Time complexity O\(n logn\)
   2. Space complexity O\(1\) or O\(log n\) due recursion stack

## Solution

```java
class Solution {
    public ListNode sortList(ListNode head) {
        List<Integer> list = new ArrayList<>();
        ListNode cur = head;
        while (cur != null) {
            list.add(cur.val);
            cur = cur.next;
        }
        Collections.sort(list);
        cur = head;
        for (int val : list) {
            cur.val = val;
            cur = cur.next;
        }
        return head;
    }
}
```

```java
class Solution {
    public ListNode sortList(ListNode head) {
        if (head == null || head.next == null) return head;

        ListNode slow = head, fast = head.next.next;
        while (fast!= null && fast.next!= null){
            slow = slow.next;
            fast = fast.next.next;
        }
        ListNode l1 = sortList(slow.next);
        slow.next = null;
        ListNode l2 = sortList(head);
        return merge(l1, l2);
    }

    private ListNode merge(ListNode l1, ListNode l2){
        ListNode dummy = new ListNode(-1);
        ListNode cur = dummy;
        while (l1 != null || l2 != null){
            if (l1 == null){
                cur.next = l2;
                break;
            } else if (l2 == null){
                cur.next = l1;
                break;
            } else {
                if (l1.val < l2.val){
                    cur.next = l1;
                    l1 = l1.next;
                } else {
                    cur.next = l2;
                    l2 = l2.next;
                }
                cur = cur.next;
            }
        }
        return dummy.next;
    }
}
```

## Additional {#additional}

