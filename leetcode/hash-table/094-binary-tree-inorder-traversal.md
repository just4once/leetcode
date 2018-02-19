### Question {#question}

[https://leetcode.com/problems/binary-tree-inorder-traversal/description/](https://leetcode.com/problems/binary-tree-inorder-traversal/description/)

Given a binary tree, return the inorder traversal of its nodes' values.

**Example:**

```
Given binary tree [1,null,2,3],
   1
    \
     2
    /
   3
return [1,3,2].
```

### Thought Process {#thought-process}

1. Recursion
   1. Time complexity O\(n\)
   2. Space complexity O\(n\), and extra space due to recursion is O\(log n\), worst time O\(log n\) when the tree is like linked list
2. Stack
   1. While current node has left leaf, we need to store them to the stack for later exploration
   2. Then pull a node out of the stack, if there is right leaf we need to its left leaf as well
   3. Time complexity O\(n\)
   4. Space complexity O\(n\)
3. Morris Traversal
   1. In place travel of tree, where we initialize the current as root
   2. If the cur has no left child, we can add the node to the result, since it's smallest node
   3. If the cur has left child, we need to find the rightmost node of the left child, so we can add cur to it, so it's in order, now we need to clear the left child for cur, and reset the cur to the original left child, and continue the process
   4. Time complexity O\(n\)
   5. Space complexity O\(n\), and O\(1\) extra

### Solution

Recursion

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        getNode(list, root);
        return list;
    }

    private void getNode(List<Integer> list, TreeNode node){
        if(node == null) return;
        getNode(list, node.left);
        list.add(node.val);
        getNode(list, node.right);
    }
}
```

Stack

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        TreeNode cur = root;
        while (cur != null || !stack.isEmpty()) {
            while (cur != null) {
                stack.push(cur);
                cur = cur.left;
            }
            cur = stack.pop();
            list.add(cur.val);
            cur = cur.right;
        }
        return list;
    }
}
```

Morris Traversal

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        TreeNode cur = root, pre = null;
        while (cur != null) {
            if (cur.left == null) {
                list.add(cur.val);
                cur = cur.right;
            } else {
                pre = cur.left;
                while (pre.right != null) {
                    pre = pre.right;
                }
                pre.right = cur;
                TreeNode tmp = cur.left;
                cur.left = null;
                cur = tmp;
            }
        }
        return list;
    }
}
```

### Additional {#additional}



