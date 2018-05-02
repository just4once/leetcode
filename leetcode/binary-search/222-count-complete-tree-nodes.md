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
   1. At each root, we get the height and its right child, where the height is based on traversal to the left
   2. If the rightHeight + 1 == height, it means that we have left part completely full \(the height function get to travel to the middle of last level\), then the count = \(1 &lt;&lt; \(h - 1\)\) + countNodes\(root.right\)
   3. Otherwise, the right part is completely full, so the count = \(1 &lt;&lt; \(h - 2\)\) + countNodes\(root.left\)
   4. Time complexity O\(\(logn\)^2\)
   5. Space complexity O\(logn\) due to recursion
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

```java
class Solution { 
    public int countNodes(TreeNode root) {
        if (root == null) return 0;
        int h = getHeight(root);
        int rightH = getHeight(root.right);
        // left half is complete
        if (h == rightH + 1) return (1 << (h - 1)) + countNodes(root.right);
        // right half is complete
        else return (1 << (h - 2)) + countNodes(root.left);
    }
    
    private int getHeight(TreeNode root) {
        if (root == null) return 0;
        else return 1 + getHeight(root.left);
    }
}
```

```java
class Solution { 
    public int countNodes(TreeNode root) {
        int h = getHeight(root), count = 0;
        while (h > 0) {
            int rightH = getHeight(root.right);
            // left part is complete
            if (h == rightH + 1) {
                root = root.right;
                count += 1 << (h - 1);
            } else {
                root = root.left;
                count += 1 << (h - 2);
            }
            h--;
        }
        return count;
    }
    
    private int getHeight(TreeNode root) {
        if (root == null) return 0;
        else return 1 + getHeight(root.left);
    }
}
```

### Additional {#additional}



