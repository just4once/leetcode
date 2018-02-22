### Question {#question}

[https://leetcode.com/problems/contains-duplicate-ii/description/](https://leetcode.com/problems/contains-duplicate-ii/description/)

Given an array of integers and an integer k, find out whether there are two distinct indices i and j in the array such that **nums\[i\] = nums\[j\]** and the **absolute **difference between i and j is at most k.

**Example:**

```

```

### Thought Process {#thought-process}

1. Brute Force - Check the range of K \(TLE\)
   1. Two pointers tracking the start and end points
   2. Time complexity O\(n min\(k, n\)\)
   3. Space complexity O\(1\)
2. Hash Table
   1. Use map to store the number and its index to find the difference at O\(1\) time, Or Set to keep size of range for comparison
   2. Time complexity O\(n\)
   3. Space complexity O\(n\), and O\(min\(n. k\)\) for set
3. Separate Class - Sorting
   1. Create a separate class node to store the value and its index
   2. After sorting, we simply check the node's index with its previous element's index is within the range of k
   3. Default library arrays sort use merge sort for objects, so it's stable, so we don't need to include the index in the compareTo function
   4. Time complexity O\(n logn\)
   5. Space complexity O\(n\)

### Solution

Brute Force

```java
class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        for (int i = 1 ; i < nums.length; i++) {
            for (int j = Math.max(0, i - k); j < i; j++) {
                if (nums[i] == nums[j]) return true;
            }
        }
        return false;
    }
}
```

Hash Table

```java
class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            if (map.containsKey(nums[i]) && i - map.get(nums[i]) <= k) return true;
            map.put(nums[i], i);
        }
        return false;
    }
}
```

```java
class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        Set<Integer> set = new HashSet<>();
        for (int i = 0; i < nums.length; i++) {
            if (i > k) set.remove(nums[i - k - 1]);
            if (!set.add(nums[i])) return true;
        }
        return false;
    }
}
```

Separate Node

```java
class Solution {
    private static class Node implements Comparable<Node> {
        private int value, index;
        public Node(int value, int index) {
            this.value = value;
            this.index = index;
        }

        public int compareTo(Node that) {
            return this.value - that.value;
        }
    }

    public boolean containsNearbyDuplicate(int[] nums, int k) {
        int n = nums.length;
        Node[] nodes = new Node[n];
        for (int i = 0; i < n; i++) {
            nodes[i] = new Node(nums[i], i);
        }
        Arrays.sort(nodes);
        for (int i = 1; i < n; i++) {
            if (nodes[i].value == nodes[i - 1].value && nodes[i].index - nodes[i - 1].index <= k) return true;
        }
        return false;
    }
}
```

### Additional {#additional}



