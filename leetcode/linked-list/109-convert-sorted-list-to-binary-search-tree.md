### Question {#question}

Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

**Example:**

```
Given the sorted linked list: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

      0
     / \
   -3   9
   /   /
 -10  5
```

### Thought Process {#thought-process}

1. List
   1. Add the value to the list and create left and right part
   2. Time complexity O\(n\)
   3. Space complexity O\(n\)
2. asd

### Solution

```java
class Solution {
    public TreeNode sortedListToBST(ListNode head) {
        List<Integer> list = new ArrayList<>();
        ListNode cur = head;
        while(cur != null){
            list.add(cur.val);
            cur = cur.next;
        }
        return buildNode(list, 0, list.size() - 1);
    }

    public TreeNode buildNode(List<Integer> list, int lo, int hi){
        if (lo > hi) return null;
        int mid = lo + (hi - lo)/2;
        TreeNode node = new TreeNode(list.get(mid));
        node.left = buildNode(list, lo, mid - 1);
        node.right = buildNode(list, mid + 1, hi);
        return node;
    }
}
```

```java
class Solution {
    public TreeNode sortedListToBST(ListNode head) {
        return toBST(head, null);
    }
    public TreeNode toBST(ListNode head, ListNode tail){
        if(head == tail) return null;
        ListNode slow = head;
        ListNode fast = head;
        while (fast != tail && fast.next != tail) {
            slow = slow.next;
            fast = fast.next.next;
        }
        TreeNode root = new TreeNode(slow.val);
        root.left = toBST(head, slow);
        root.right = toBST(slow.next, tail);
        return root;
    }
}
```

### Additional {#additional}



