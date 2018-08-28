# 725-split-linked-list-in-parts

## Question {#question}

Given a \(singly\) linked list with head node root, write a function to split the linked list into k consecutive linked list "parts".

The length of each part should be as equal as possible: no two parts should have a size differing by more than 1. This may lead to some parts being null.

The parts should be in order of occurrence in the input list, and parts occurring earlier should always have a size greater than or equal parts occurring later.

Return a List of ListNode's representing the linked list parts that are formed.

Examples 1-&gt;2-&gt;3-&gt;4, k = 5 // 5 equal parts \[ \[1\], \[2\], \[3\], \[4\], null \]

**Example 1:**

```text
Input: 
root = [1, 2, 3], k = 5
Output: [[1],[2],[3],[],[]]
Explanation:
The input and each element of the output are ListNodes, not arrays.
For example, the input root has root.val = 1, root.next.val = 2, \root.next.next.val = 3, and root.next.next.next = null.
The first element output[0] has output[0].val = 1, output[0].next = null.
The last element output[4] is null, but it's string representation as a ListNode is [].
```

**Example 2:**

```text
Input: 
root = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10], k = 3
Output: [[1, 2, 3, 4], [5, 6, 7], [8, 9, 10]]
Explanation:
The input has been split into consecutive parts with size difference at most 1, and earlier parts are a larger size than the later parts.
```

**Note:**    


* The length of root will be in the range \[0, 1000\].
* Each value of a node in the input will be an integer in the range \[0, 999\].
* k will be an integer in the range \[1, 50\].

## Thought Process {#thought-process}

1. Create New List
   1. Each part has n / k elements except first n % k parts will have an extra element
   2. Time complexity O\(n + k\)
   3. Space complexity O\(max\(n, k\)\)
2. Break the list
   1. Instead of create new list, we can break it
   2. Time complexity O\(n + k\)
   3. Space complexity O\(k\)

## Solution

```java
class Solution {
    public ListNode[] splitListToParts(ListNode root, int k) {
        ListNode[] res = new ListNode[k];
        if (k == 1) {
            res[0] = root;
            return res;
        }
        int n = getLength(root);
        ListNode pre = null;
        for (int i = 0; i < k; i++) {
            res[i] = root;
            int j = n / k + (i < n % k ? 1 : 0);
            while (root != null && j > 0) {
                pre = root;
                root = root.next;
                j--;
            }
            if (pre != null) pre.next = null;
        }
        return res;
    }

    private int getLength(ListNode root) {
        int len = 0;
        while (root != null) {
            len++;
            root = root.next;
        }
        return len;
    }
}
```

## Additional {#additional}

