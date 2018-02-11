### Question {#question}

Given preorder and inorder traversal of a tree, construct the binary tree.

**Note:**

You may assume that duplicates do not exist in the tree.

**Example:**

```
preorder = [3,9,20,15,7]
inorder = [9,3,15,20,7]

    3
   / \
  9  20
    /  \
   15   7
```

### Thought Process {#thought-process}

1. Divide Array to Left and Right part
   1. Preorder reaches the root first, then its left subtree
   2. Inorder reaches the left most leaf, than its parent, sibling, and finally return to the parent
   3. Then we find the index of root in the inorder, and repeat the same process
   4. Time complexity O\(n^2\)
   5. Space complexity O\(n\), O\(1\) extra
2. Optimized the index search
   1. Time complexity O\(n\)
   2. Space complexity O\(n\), O\(n\) extra
3. Further Optimized with global variables to check the index of inorder and preorder
   1. We travel as far left as possible, increment the index of preorder as we go
   2. After left subtree is complete, we are ready to move on to the next value, we increment the index of inorder
   3. Then we move on to the right subtree
   4. Time complexity O\(n\)
   5. Space complexity O\(n\), O\(1\) extra

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
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        return build(preorder, 0, preorder.length -  1, inorder, 0, inorder.length - 1);
    }
    
    private TreeNode build(int[] preorder, int pLo, int pHi, int[] inorder, int inLo, int inHi) {
        if (pLo > pHi) return null;
        if (pLo == pHi) return new TreeNode(preorder[pLo]);
        TreeNode root = new TreeNode(preorder[pLo]);
        int inId = -1;
        for (int i = inLo; i <= inHi; i++) {
            if (inorder[i] == preorder[pLo]) {
                inId = i;
                break;
            }
        }
        // (inId - inLo) is number of left elements
        root.left = build(preorder, pLo + 1, pLo + inId - inLo, inorder, inLo, inId - 1);
        root.right = build(preorder, pLo + inId - inLo + 1, pHi, inorder, inId + 1, inHi);
        return root;
    }
}
```

```java
class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        if (preorder.length == 0 || preorder.length != inorder.length) return null;
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0 ; i < inorder.length; i++) {
            map.put(inorder[i], i);
        }
        return build(preorder, 0, inorder, 0, inorder.length - 1, map);
    }
    
    private TreeNode build(int[] preorder, int pLo, int[] inorder, int inLo, int inHi, Map<Integer, Integer> map) {
        if (inLo > inHi) return null;
        if (inLo == inHi) return new TreeNode(preorder[pLo]);
        TreeNode root = new TreeNode(preorder[pLo]);
        int inId = map.get(root.val);
        // (inId - inLo) is number of left elements
        root.left = build(preorder, pLo + 1, inorder, inLo, inId - 1, map);
        root.right = build(preorder, pLo + inId - inLo + 1, inorder, inId + 1, inHi, map);
        return root;
    }
}
```

```java
class Solution {
    int pId = 0, iId = 0;
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        if (preorder.length == 0 || preorder.length != inorder.length) return null;
        return build(preorder, inorder, Integer.MAX_VALUE);
    }
    
    private TreeNode build(int[] preorder, int[] inorder, int rootValue) {
        if (iId == inorder.length || inorder[iId] == rootValue) return null;
        TreeNode node = new TreeNode(preorder[pId]);
        pId++;
        node.left = build(preorder, inorder, node.val);
        iId++;
        node.right = build(preorder, inorder, rootValue);
        return node;
    }
}
```

```java
class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        if (preorder.length == 0 || preorder.length != inorder.length) return null;
        Stack<TreeNode> stack = new Stack<>();
        TreeNode root = new TreeNode(preorder[0]), cur = root;
        for (int pId = 1, iId = 0; pId < preorder.length; pId++) {
            if (inorder[iId] != cur.val) {
                cur.left = new TreeNode(preorder[pId]);
                stack.push(cur);
                cur = cur.left;
            } else {
                iId++;
                while (!stack.isEmpty() && stack.peek().val == inorder[iId]) {
                    cur = stack.pop();
                    iId++;
                }
                cur.right = new TreeNode(preorder[pId]);
                cur = cur.right;
            }
        }
        return root;
    }
}
```

### Additional {#additional}



