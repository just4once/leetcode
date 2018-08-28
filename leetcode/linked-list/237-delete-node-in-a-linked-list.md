# 237-delete-node-in-a-linked-list

## Question {#question}

[https://leetcode.com/problems/delete-node-in-a-linked-list/description/](https://leetcode.com/problems/delete-node-in-a-linked-list/description/)

Write a function to delete a node \(except the tail\) in a singly linked list, given only access to that node.

Supposed the linked list is`1 -> 2 -> 3 -> 4`and you are given the third node with value`3`, the linked list should become`1 -> 2 -> 4`after calling your function.

**Example:**

```text

```

## Thought Process {#thought-process}

1. Copy val
   1. Since we don't have access to the previous node, we have to do something with current node
   2. By copying the value of next, we are able to "delete" current node and link current to next's next
   3. Time complexity O\(1\)
   4. Space complexity O\(1\)

## Solution

```java
class Solution {
    public void deleteNode(ListNode node) {
        node.val = node.next.val;
        node.next = node.next.next;
    }
}
```

## Additional {#additional}

