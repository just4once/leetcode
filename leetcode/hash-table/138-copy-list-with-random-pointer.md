### Question {#question}

A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a deep copy of the list.

**Example:**

```

```

### Thought Process {#thought-process}

1. Recursion
   1. We simply construct the listnode by recursion
   2. We need a map to store the mapping between the node and its clone, so when the next and random points to a node we already created, we can just return from the map
   3. Time complexity O\(n\)
   4. Space complexity O\(n\) from recursion stack and map
2. Iterative
   1. Time complexity O\(n\)
   2. Space complexity O\(n\), O\(n\) extra
3. Weaving
   1. Insert the clone between the current element, and its next element, so the list looks like cur -&gt; curClone -&gt; n1 -&gt; n1Clone
   2. Assign the random pointer as we run again through the list;
   3. Link for the clone and revert the link for original nodes
   4. Time complexity O\(n\)
   5. Space complexity O\(n\), O\(1\) extra

### Solution

```java
/**
 * Definition for singly-linked list with a random pointer.
 * class RandomListNode {
 *     int label;
 *     RandomListNode next, random;
 *     RandomListNode(int x) { this.label = x; }
 * };
 */
public class Solution {
    public RandomListNode copyRandomList(RandomListNode head) {
        Map<RandomListNode, RandomListNode> map = new HashMap<>();
        return buildR(head, map);
    }
    
    private RandomListNode buildR(RandomListNode head, Map<RandomListNode, RandomListNode> map) {
        if (head == null) return null;
        if (map.containsKey(head)) return map.get(head);
        RandomListNode newHead = new RandomListNode(head.label);
        map.put(head, newHead);
        newHead.next = buildR(head.next, map);
        newHead.random = buildR(head.random, map);
        return newHead;
    }
}
```

```java
public class Solution {
    public RandomListNode copyRandomList(RandomListNode head) {
        Map<RandomListNode, RandomListNode> map = new HashMap<>();
        RandomListNode cur = head;
        while (cur != null) {
            map.put(cur, new RandomListNode(cur.label));
            cur = cur.next;
        }
        cur = head;
        while (cur != null) {
            map.get(cur).next = map.get(cur.next);
            map.get(cur).random = map.get(cur.random);
            cur = cur.next;
        }
        return map.get(head);
    }
}
```

```java
public class Solution {
    public RandomListNode copyRandomList(RandomListNode head) {
        RandomListNode cur = head, next = null;
        // Interweaving the node and its clone
        while (cur != null) {
            next = cur.next;
            cur.next = new RandomListNode(cur.label);
            cur.next.next = next;
            cur = next;
        }
        // assing the random pointer
        cur = head;
        while (cur != null) {
            if (cur.random != null) cur.next.random = cur.random.next;
            cur = cur.next.next;
        }
        // create link for new nodes, and revert the link for originals
        cur = head;
        RandomListNode dummy = new RandomListNode(0);
        dummy.next = cur;
        next = dummy;
        while (cur != null) {
            next.next = cur.next;
            cur.next = cur.next.next;
            next = next.next;
            cur = cur.next;
        }
        return dummy.next;
    }
}
```

### Additional {#additional}



