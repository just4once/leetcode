### Question {#question}

[https://leetcode.com/problems/intersection-of-two-linked-lists/description/](https://leetcode.com/problems/intersection-of-two-linked-lists/description/)

Write a program to find the node at which the intersection of two singly linked lists begins.



**Example:**

```
A:          a1 → a2
                   ↘
                     c1 → c2 → c3
                   ↗            
B:     b1 → b2 → b3
```

begin to intersect at node c1.

Notes:

* If the two linked lists have no intersection at all, return null.
* The linked lists must retain their original structure after the function returns.
* You may assume there are no cycles anywhere in the entire linked structure.
* Your code should preferably run in O\(n\) time and use only O\(1\) memory.

### Thought Process {#thought-process}

1. Set
   1. Add all the node to hashset from list A
   2. checking the node exist in the hashset or not
   3. Time complexity O\(m\)
   4. Space complexity O\(m + n\)
2. Two Pointers
   1. Each pointer points to the start of the list, pA and pB
   2. When pA reach the end, we reinitialize to head of B, opposite thing happens for pB
   3. If the end of list for A and B is not the same, we have no intersection
   4. Otherwise, they will eventually meet

### Solution

```java
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        Set<ListNode> set = new HashSet<>();
        while (headA != null){
            set.add(headA);
            headA = headA.next;
        }
        while (headB != null){
            if (set.contains(headB)) return headB;
            headB = headB.next;
        }
        return null;
    }
}
```

```java
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if (headA == null || headB == null) return null;
        ListNode pA = headA, pB = headB;
        while (pA != pB) {
            pA = pA == null ? headB : pA.next;
            pB = pB == null ? headA : pB.next;
        }
        return pA;
    }
}
```

### Additional {#additional}



