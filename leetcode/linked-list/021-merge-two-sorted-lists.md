# 021-merge-two-sorted-lists

## Question {#question}

[https://leetcode.com/problems/merge-two-sorted-lists/description/](https://leetcode.com/problems/merge-two-sorted-lists/description/)

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

**Example:**

```text
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```

## Thought Process {#thought-process}

1. Two Pointers - Iterative
   1. Two pointers for each list, we link the node until both pointers reach the end
   2. Time complexity O\(m + n\)
   3. Space complexity O\(1\) or O\(m + n\) if we have to create new list
2. Recursive
   1. Time complexity O\(m + n\)
   2. Space complexity O\(1\)

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
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0);
        ListNode cur = dummy;
        while(l1!=null || l2!=null){
            if(l1 == null){
                while(l2!=null){
                    cur.next = new ListNode(l2.val);
                    l2 = l2.next;
                    cur = cur.next;
                }
                break;
            }
            if(l2 == null){
                while(l1!=null){
                    cur.next = new ListNode(l1.val);
                    l1 = l1.next;
                    cur = cur.next;
                }
                break;
            }
            if(l1.val <= l2.val){
                cur.next = new ListNode(l1.val);
                l1 = l1.next;
            } else{
                cur.next = new ListNode(l2.val);
                l2 = l2.next;
            }
            cur = cur.next;
        }
        return dummy.next;
    }
}
```

```java
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    if(l2 == null) return l1;
    if(l2 == null) return l1;
    ListNode head;
    if(l1.val <= l2.val) {
        head = l1;
        head.next = mergeTwoLists(l1.next, l2);
    }else {
        head = l2;
        head.next = mergeTwoLists(l1, l2.next);
    }
    return head;
    }
}
```

## Additional {#additional}

