### Question {#question}

[https://leetcode.com/problems/trapping-rain-water/description/](https://leetcode.com/problems/trapping-rain-water/description/)

Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

**Example:**

```
Given [0,1,0,2,1,0,1,3,2,1,2,1], return 6
```

### ![](/assets/041.png) {#thought-process}

### Thought Process {#thought-process}

1. Brute Force
   1. For each element find it's max left boundary and right boundary
   2. The min of boundary decide how much water a column can store
   3. Deduct the height of current element, we got the amount of water can be stored at this index
   4. Time complexity O\(n^2\)
   5. Space complexity O\(1\)
2. Optimized Brute Force - Two passes
   1. Instead keep search for its boundary, we can use cache to store the boundary
   2. Another optimization, we can make is that instead of use two passes to create left and right boundary cache, we can create left boundary on the go
   3. Time complexity O\(n\)
   4. Space complexity O\(n\)
3. One pass
   1. Instead of use one pass to store the right boundary, we can use two pointers to track of boundaries
   2. As long as the one boundary is higher, we can accumulate the water from the opposite side
   3. Once the higher boundary switch side, we switch to the other side and start accumulate water
   4. Time complexity O\(n\)
   5. Space complexity O\(1\)

### Solution

```java
class Solution {
    public int trap(int[] height) {
        if (height == null || height.length <= 1) return 0;
        int n = height.length;
        int[] right = new int[n];
        right[n - 1] = height[n - 1];
        int rightMax = right[n - 1];
        for (int i = n - 2; i >= 0; i--) {
            rightMax = Math.max(rightMax, height[i]);
            right[i] = rightMax;
        }
        int leftMax = Integer.MIN_VALUE;
        int water = 0;
        for (int i = 0; i < n; i++) {
            leftMax = Math.max(leftMax, height[i]);
            water += Math.min(leftMax, right[i]) - height[i];
        }
        return water;
    }
}
```

One pass

```java
class Solution {
    public int trap(int[] height) {
        if (height == null || height.length <= 1) return 0;
        int n = height.length;
        int left = 0, right = 0;
        int lo = 0, hi = n - 1;
        int water = 0;
        while (lo < hi) {
            left = Math.max(left, height[lo]);
            right = Math.max(right, height[hi]);
            if (left > right) {
                water += right - height[hi];
                hi--;
            } else {
                water += left - height[lo];
                lo++;
            }
        }
        return water;
    }
}
```

### Additional {#additional}



