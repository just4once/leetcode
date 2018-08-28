# 023-merge-k-sorted-lists

## Question {#question}

[https://leetcode.com/problems/merge-k-sorted-lists/description/](https://leetcode.com/problems/merge-k-sorted-lists/description/)

Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

**Example:**

```text

```

## Thought Process {#thought-process}

1. Brute Force
   1. Append all the values to the array list and sort
   2. Time complexity O\(n logn\)
   3. Space complexity O\(n\), or O\(n\) depends on new list is created
2. K pointers
   1. Compare the head of the list one by one
   2. Space complexity O\(kn\), where n is total number of node
   3. Space complexity O\(1\), or O\(n\) depends on new list is created
3. Min Heap
   1. Store the list in the min heap, and build the list as we poll out the min node
   2. Time complexity O\(n logk\)
   3. Space complexity O\(n\)
4. Divide and Conquer
   1. Divide the list into left and right part
   2. Merge the sorted part
   3. Time complexity O\(n logk\)
   4. Space complexity O\(log k\) for recursion stack

## Solution

Brute Force

```java
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        List<Integer> vals = new ArrayList<>();
        for (ListNode list : lists) {
            while (list != null) {
                vals.add(list.val);
                list = list.next;
            }
        }
        Collections.sort(vals);
        ListNode dummy = new ListNode(0), cur = dummy;
        for (int val : vals) {
            cur.next = new ListNode(val);
            cur = cur.next;
        }
        return dummy.next;
    }
}
```

Min Heap

```java
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        Queue<ListNode> minHeap = new PriorityQueue<>((a, b) -> a.val - b.val);
        for (ListNode list : lists) {
            if (list != null) minHeap.offer(list);
        }
        ListNode dummy = new ListNode(0), cur = dummy;
        while (!minHeap.isEmpty()) {
            ListNode top = minHeap.poll();
            cur.next = new ListNode(top.val);
            cur = cur.next;
            if (top.next != null) minHeap.offer(top.next);
        }
        return dummy.next;
    }
}
```

Divide and Conquer

```java
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists == null || lists.length == 0) return null;
        return mergeR(lists, 0, lists.length - 1);
    }

    private ListNode mergeR(ListNode[] lists, int i, int j) {
        if (i == j) return lists[i];
        int k = i + (j - i) / 2;
        ListNode left = mergeR(lists, i, k);
        ListNode right = mergeR(lists, k + 1, j);
        return merge(left, right);
    }

    private ListNode merge(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0), cur = dummy;
        while (l1 != null || l2 != null) {
            if (l1 == null) {
                cur.next = clone(l2);
                break;
            } else if (l2 == null) {
                cur.next = clone(l1);
                break;
            } else if (l1.val <= l2.val) {
                cur.next = new ListNode(l1.val);
                l1 = l1.next;
            } else {
                cur.next = new ListNode(l2.val);
                l2 = l2.next;
            }
            cur = cur.next;
        }
        return dummy.next;
    }

    private ListNode clone(ListNode l) {
        ListNode dummy = new ListNode(0), cur = dummy;
        while (l != null) {
            cur.next = new ListNode(l.val);
            l = l.next;
            cur = cur.next;
        }
        return dummy.next;
    }
}
```

## Additional {#additional}

