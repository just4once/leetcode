# 426-convert-binary-search-tree-to-sorted-doubly-linked-list

## Question {#question}

Convert a BST to a sorted circular doubly-linked list in-place. Think of the left and right pointers as synonymous to the previous and next pointers in a doubly-linked list.

Let's take the following BST as an example, it may help you understand the problem better: 

![](https://leetcode.com/static/images/problemset/BSTDLLOriginalBST.png)

We want to transform this BST into a circular doubly linked list. Each node in a doubly linked list has a predecessor and successor. For a circular doubly linked list, the predecessor of the first element is the last element, and the successor of the last element is the first element.

The figure below shows the circular doubly linked list for the BST above. The "head" symbol means the node it points to is the smallest element of the linked list. 

![](https://leetcode.com/static/images/problemset/BSTDLLReturnDLL.png)

Specifically, we want to do the transformation in place. After the transformation, the left pointer of the tree node should point to its predecessor, and the right pointer should point to its successor. We should return the pointer to the first element of the linked list.

The figure below shows the transformed BST. The solid line indicates the successor relationship, while the dashed line means the predecessor relationship. 

![](https://leetcode.com/static/images/problemset/BSTDLLReturnBST.png)



## Thought Process {#thought-process}

1. Inorder traversal
   1. To double link the node, we need inorder traversal to get them in the right order
   2. We also need a previous node to be able to make the connection to the next node
   3. To facilitate the double linking, we create a dummy node at first, which help us in returning the smallest node and also save the reference for linkage between the smallest node and largest node
   4. For inorder\(root\) function, we create link as follow
      1. pre.right = root
      2. root.left = pre
      3. pre = root \(for next linkage\)
   5. At the end, we need to make sure the lastNode.right = firstNode and firstNode.left = lastNode
   6. Time complexity O\(n\)
   7. Space complexity O\(logn\)
2. asd

## Solution

```java
class Solution {
    Node pre;
    
    public Node treeToDoublyList(Node root) {
        // we basically need to do an in-order traversal
        // we find the left most node
        if (root == null) return null;
        Node dummy = new Node(0, null, null);
        pre = dummy;
        inorder(root);
        pre.right = dummy.right;
        dummy.right.left = pre;
        dummy.right = null;
        return pre.right;
    }
    
    private void inorder(Node cur) {
        if (cur == null) return;
        inorder(cur.left);
        pre.right = cur;
        cur.left = pre;
        pre = cur;
        inorder(cur.right);
    }
}
```

## Additional {#additional}

