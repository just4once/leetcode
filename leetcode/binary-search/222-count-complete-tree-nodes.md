### Question {#question}

[https://leetcode.com/problems/count-complete-tree-nodes/description/](https://leetcode.com/problems/count-complete-tree-nodes/description/)

Given a **complete **binary tree, count the number of nodes.

**Definition of a complete binary tree from **[**Wikipedia**](http://en.wikipedia.org/wiki/Binary_tree#Types_of_binary_trees)**:**  
In a complete binary tree every level, except possibly the last, is completely filled, and all nodes in the last level are as far left as possible. It can have between 1 and 2hnodes inclusive at the last level h.

**Example:**

```

```

### Thought Process {#thought-process}

1. DFS
   1. We travel the tree to the left and right at the same time
   2. If the tree is full tree, we can return the \(1 &lt;&lt; height\) - 1, otherwise we need to search the left and right separately and + 1
   3. Time complexity O\(\(logn\)^2\), due to half of traversal is skipped and height function is O\(logn\)
   4. Space complexity O\(logn\) due to recursion stack
2. Recursion
3. Iterative

### Solution

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution { 
    public int countNodes(TreeNode root) {
        if (root == null) return 0;
        TreeNode left = root, right = root;
        int height = 0;
        while (right != null) {
            left = left.left;
            right = right.right;
            height++;
        }
        // the tree is a full tree
        if (left == null) return (1 << height) - 1;
        else return 1 + countNodes(root.left) + countNodes(root.right);
    }
}
```

### Additional {#additional}



