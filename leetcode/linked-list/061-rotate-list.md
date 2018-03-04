### Question {#question}

Given a list, rotate the list to the right by k places, where k is non-negative.

**Example:**

```
Given 1->2->3->4->5->NULL and k = 2,

return 4->5->1->2->3->NULL.
```

### Thought Process {#thought-process}

1. Circular Linked List
   1. Count the size of linked list, create the link between the tail and the first node
   2. Mod the k with the size, since a full size rotation goes back to the same list
   3. Move the pointer, pointed at the old tail right now, size - k steps forward to point at the new tail
   4. Unset the link and return the newHead
   5. Time complexity O\(n\)
   6. Space complexity O\(1\)

### Solution

```java
class Solution {
    public ListNode rotateRight(ListNode head, int k) {
        if(head == null) return head;
        int size = 1;
        ListNode cur = head;
        while(cur.next != null){
            size++;
            cur = cur.next;
        }
        k %= size;
        if(k == 0) return head;
        cur.next = head; //circular ListNode
        while (size-- > k) cur = cur.next;
        head = cur.next;
        cur.next = null;
        return head;
    }
}
```

### Additional {#additional}



