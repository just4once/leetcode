# 314-binary-tree-vertical-order-traversal

## Question {#question}

[https://leetcode.com/problems/binary-tree-vertical-order-traversal/description/](https://leetcode.com/problems/binary-tree-vertical-order-traversal/description/)

Given a binary tree, return thevertical ordertraversal of its nodes' values. \(ie, from top to bottom, column by column\).

If two nodes are in the same row and column, the order should be from **left to right**.

**Example:**

```text
Given binary tree [3,9,8,4,0,1,7],
     3
    /\
   /  \
   9   8
  /\  /\
 /  \/  \
 4  01   7
 return its vertical order traversal as:
 [
  [4],
  [9],
  [3,0,1],
  [8],
  [7]
]
```

## Thought Process {#thought-process}

1. BFS
   1. Use queue to store the col index and treenode
   2. As we poll the node out, we index the left with curIndex - 1 and right with curIndex  + 1
   3. We can also count the range first, and then do the thing in one pass
   4. Time complexity O\(n\)
   5. Space complexity O\(n\)
2. BFS - TreeMap
   1. Time complexity O\(n logn\)
   2. Space complexity O\(n\)

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
    public List<List<Integer>> verticalOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if (root == null) return res;
        Queue<TreeNode> q = new LinkedList<>();
        Queue<Integer> cols = new LinkedList<>();
        Map<Integer, List<Integer>> map = new HashMap<>();
        q.offer(root);
        cols.offer(0);
        int min = 0, max = 0;
        while (!q.isEmpty()) {
            TreeNode cur = q.poll();
            int col = cols.poll();
            if (!map.containsKey(col)) map.put(col, new ArrayList<>());
            map.get(col).add(cur.val);
            if (cur.left != null) {
                q.offer(cur.left);
                cols.offer(col - 1);
                min = Math.min(min, col - 1);
            }
            if (cur.right != null) {
                q.offer(cur.right);
                cols.offer(col + 1);
                max = Math.max(max, col + 1);
            }
        }
        for (int i = min; i <= max; i++) {
            res.add(map.get(i));
        }
        return res;
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
    public List<List<Integer>> verticalOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if (root == null) return res;
        Queue<TreeNode> q = new LinkedList<>();
        Queue<Integer> cols = new LinkedList<>();
        Map<Integer, List<Integer>> map = new TreeMap<>();
        q.offer(root);
        cols.offer(0);
        int min = 0, max = 0;
        while (!q.isEmpty()) {
            TreeNode cur = q.poll();
            int col = cols.poll();
            if (!map.containsKey(col)) map.put(col, new ArrayList<>());
            map.get(col).add(cur.val);
            if (cur.left != null) {
                q.offer(cur.left);
                cols.offer(col - 1);
                min = Math.min(min, col - 1);
            }
            if (cur.right != null) {
                q.offer(cur.right);
                cols.offer(col + 1);
                max = Math.max(max, col + 1);
            }
        }
        res.addAll(map.values());
        return res;
    }
}
```

## Additional {#additional}

