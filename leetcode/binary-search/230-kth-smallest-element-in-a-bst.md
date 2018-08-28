# 230-kth-smallest-element-in-a-bst

## Question {#question}

[https://leetcode.com/problems/kth-smallest-element-in-a-bst/description/](https://leetcode.com/problems/kth-smallest-element-in-a-bst/description/)

Given a binary search tree, write a function kthSmallest to find the kth smallest element in it.

**Note:**

You may assume k is always valid, 1 ≤ k ≤ BST's total elements.

**Follow up:**

What if the BST is modified \(insert/delete operations\) often and you need to find the kth smallest frequently? How would you optimize the kthSmallest routine?

**Example:**

```text

```

## Thought Process {#thought-process}

1. In-Order Traversal
   1. We have a counter to count how many elements we have encounters during the in order travel
   2. We can use stack for iterative approach, arraylist or global varibles for recursion
   3. Time complexity O\(logn\)
   4. Space complexity O\(k\) or O\(1\), and O\(logn\) for recursion stack

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
    public int kthSmallest(TreeNode root, int k) {
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
            if (list.size() == k) break;
            if (cur.right != null) {
                cur = cur.right;
                continue;
            }
            cur = null;
        }
        return list.get(k - 1);
    }
}
```

```java
class Solution {
    public int kthSmallest(TreeNode root, int k) {
        List<Integer> list = new ArrayList<>();
        inorder(list, root, k);
        return list.get(k - 1);
    }

    private void inorder(List<Integer> list, TreeNode node, int k) {
        if (node == null || list.size() == k) return;
        inorder(list, node.left, k);
        list.add(node.val);
        inorder(list, node.right, k);
    }
}
```

```java
class Solution {
    private int i = 0, v = 0;
    public int kthSmallest(TreeNode root, int k) {
        inorder(root, k);
        return v;
    }

    private void inorder(TreeNode root, int k) {
        if (root == null || i == k)  return;
        inorder(root.left, k);
        i++;
        if (i == k) {
            v = root.val;
            return;
        }
        inorder(root.right, k);
    }
}
```

## Additional {#additional}

