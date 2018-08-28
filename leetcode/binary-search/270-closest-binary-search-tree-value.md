# 270-closest-binary-search-tree-value

## Question {#question}

[https://leetcode.com/problems/closest-binary-search-tree-value/description/](https://leetcode.com/problems/closest-binary-search-tree-value/description/)

Given a non-empty binary search tree and a target value, find the value in the BST that is closest to the target.

**Note:**

* Given target value is a floating point.
* You are guaranteed to have only one unique value in the BST that is closest to the target.

**Example:**

```text

```

## Thought Process {#thought-process}

1. Binary Search
   1. When the target is greater than the root, we search the right otherwise the left
   2. Time complexity O\(logn\)
   3. Space complexity O\(1\)

## Solution

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
    public int closestValue(TreeNode root, double target) {
        int val = root.val;
        double diff = Double.MAX_VALUE;
        while (root != null) {
            double tmp = Math.abs(root.val - target);
            if (tmp < diff) {
                val = root.val;
                diff = tmp;
            }
            if (target < root.val) root = root.left;
            else if (target > root.val) root = root.right;
            else break;
        }
        return val;
    }
}
```

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
    public int closestValue(TreeNode root, double target) {
        return closest(root, target, root.val);
    }

    private int closest(TreeNode root, double target, int current) {
        if (root == null || current == target) return current;
        if (Math.abs(root.val - target) < Math.abs(current - target)) current = root.val;
        if (root.val < target) current = closest(root.right, target, current);
        else if (root.val > target) current = closest(root.left, target, current);
        return current;
    }
}
```

## Additional {#additional}

