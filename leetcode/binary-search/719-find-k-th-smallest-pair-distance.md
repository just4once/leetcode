### Question {#question}

[https://leetcode.com/problems/find-k-th-smallest-pair-distance/description/](https://leetcode.com/problems/find-k-th-smallest-pair-distance/description/)

Given an integer array, return the k-th smallest distance among all the pairs. The distance of a pair \(A, B\) is defined as the absolute difference between A and B.

**Example:**

```
Input:
nums = [1,3,1]
k = 1
Output: 0 
Explanation:
Here are all the pairs:
(1,3) -> 2
(1,1) -> 0
(3,1) -> 2
Then the 1st smallest distance pair is (1,1), and its distance is 0.
```

**Note:  
**

1. 2 &lt;= len\(nums\) &lt;= 10000.
2. 0 &lt;= nums\[i\] &lt; 1000000.
3. 1 &lt;= k &lt;= len\(nums\) \* \(len\(nums\) - 1\) / 2.

### Thought Process {#thought-process}

1. Brute Force \(TLE\)
   1. Generate all the distance pairs through n^2 process
   2. Sort the distances and return the k-th distance by returning distance\[k - 1\]
   3. Time complexity O\(n^2\)
   4. Space complexity O\(n^2\)
2. Heap \(TLE\)
   1. Sort the nums array and save all the adjacent pairs as nodes into the minHeap
   2. Every time, we poll the min distance pair out and save the next pair
   3. After looping for k times, the top node in the heap will contain the pair with kth distance
   4. Time complexity O\(nlogn + kLogn\)
   5. Space complexity O\(n\)
3. Binary Search
   1. Since all numbers are non-negative, the kth distance must be in between \[0, max - min\]
   2. We perform binary search on this range until find a distance that has at least k pairs 

### Solution

```java
class Solution {
    public int smallestDistancePair(int[] nums, int k) {
        int n = nums.length;
        int[] distances = new int[n * (n - 1) / 2];
        int z = 0;
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                distances[z++] = Math.abs(nums[i] - nums[j]);
            }
        }
        Arrays.sort(distances);
        return distances[k - 1];
    }
}
```

```java
class Solution {
    private static class Node {
        int i, j;
        public Node(int i, int j) {
            this.i = i;
            this.j = j;
        }
    }

    public int smallestDistancePair(int[] nums, int k) {
        Arrays.sort(nums);
        PriorityQueue<Node> minHeap = new PriorityQueue<>((a, b) -> (nums[a.j] - nums[a.i]) - (nums[b.j] - nums[b.i]));
        for (int i = 0; i + 1 < nums.length; i++) {
            minHeap.offer(new Node(i, i + 1));
        }
        Node cur = null;
        while (k-- > 0) {
            cur = minHeap.poll();
            if (cur.j + 1 < nums.length) minHeap.offer(new Node(cur.i, cur.j + 1));
        }
        return nums[cur.j] - nums[cur.i];
    }
}
```

### Additional {#additional}



