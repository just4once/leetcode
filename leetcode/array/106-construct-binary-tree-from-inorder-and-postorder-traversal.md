# 106-construct-binary-tree-from-inorder-and-postorder-traversal

## Question {#question}

[https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/description/](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/description/)

Given inorder and postorder traversal of a tree, construct the binary tree.

**Note:**

You may assume that duplicates do not exist in the tree.

**Example:**

```text
inorder = [9,3,15,20,7]
postorder = [9,15,7,20,3]

Return the following binary tree:
    3
   / \
  9  20
    /  \
   15   7
```

## Thought Process {#thought-process}

1. Inorder travels by the order of left, parent, right
2. Postorder travels by left, right, parent
3. This is similar to[105-Construct Binary Tree from Preorder and Inorder Traversal](105-construct-binary-tree-from-preorder-and-inorder-traversal.md) , unlike preorder where the root is at the front, postorder's root is at the end
4. Time complexity O\(n\)
5. Space complexity O\(n\)

## Solution

```java
class Solution {
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        if (inorder == null || inorder.length != postorder.length) return null;
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < inorder.length; i++) {
            map.put(inorder[i], i);
        }
        return build(inorder, 0, inorder.length - 1, postorder, postorder.length - 1, map);
    }

    private TreeNode build(int[] inorder, int iLo, int iHi, int[] postorder, int pHi, Map<Integer, Integer> map) {
        if (iLo > iHi) return null;
        if (iLo == iHi) return new TreeNode(inorder[iLo]);
        TreeNode root = new TreeNode(postorder[pHi]);
        int id = map.get(root.val);
        root.left = build(inorder, iLo, id - 1, postorder, pHi - (iHi - id) - 1, map);
        root.right = build(inorder, id + 1, iHi, postorder, pHi - 1, map);
        return root;
    }
}
```

```java
class Solution {
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        if (inorder == null || inorder.length == 0 || inorder.length != postorder.length) return null;
        Stack<TreeNode> stack = new Stack<>();
        int iId = inorder.length - 1, pId = iId;
        TreeNode root = new TreeNode(postorder[pId--]);
        TreeNode pre = null;
        stack.push(root);
        // because the last element is the root, and the element before the the root 
        // of its right subtree
        while (pId >= 0) {
            while (!stack.isEmpty() && stack.peek().val == inorder[iId]) {
                iId--;
                pre = stack.pop();
            }
            TreeNode node = new TreeNode(postorder[pId--]);
            if (pre != null) pre.left = node;
            else if (!stack.isEmpty()) stack.peek().right = node;
            stack.push(node);
            pre = null;
        }
        return root;
    }
}
```

```java
class Solution {
    int iId, pId;
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        if (inorder == null || inorder.length == 0 || inorder.length != postorder.length) return null;
        iId = inorder.length - 1;
        pId = iId;
        return build(inorder, postorder, null);
    }

    private TreeNode build(int[] inorder, int[] postorder, TreeNode pre) {
        if (pId < 0) return null;
        TreeNode root = new TreeNode(postorder[pId--]);
        if (root.val != inorder[iId]) root.right = build(inorder, postorder, root);
        iId--;
        if (pre == null || pre.val != inorder[iId]) root.left = build(inorder, postorder, pre);
        return root;
    }
}
```

## Additional {#additional}

