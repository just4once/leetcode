### Question {#question}

[https://leetcode.com/problems/jump-game/description/](https://leetcode.com/problems/jump-game/description/)

Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

**Example:**

```
A = [2,3,1,1,4], return true.

A = [3,2,1,0,4], return false.
```

### Thought Process {#thought-process}

1. Typical process
   1. Start with the recursive backtracking solution
   2. Optimize by using a memoization table \(top-down dynamic programming\)
   3. Remove the need for recursion \(bottom-up dynamic programming
   4. Apply final tricks to reduce the time / memory complexity
   5. Time complexity O\(2^n\), O\(n^2\), O\(n^2\)
   6. Space complexity O\(n\), O\(n\), O\(n\)
2. After bottom up approach we can see that all we care about is the first reachable index/left most good index
   1. Instead of using the array to keep track of the index, we update the good index whenever current index + its num is greater than or equal to the good index
   2. Time complexity O\(n\)
   3. Space complexity O\(1\)

### Solution

Bottom up

```java
class Solution {
    public boolean canJump(int[] nums) {
        int n = nums.length;
        boolean[] canReach = new boolean[n];
        canReach[n - 1] = true;
        for (int i = n - 2; i >=0 ; i--) {
            int bound = Math.min(nums[i] + i, n - 1);
            for (int j = i + 1; j <= bound; j++) {
                if (canReach[j]) {
                    canReach[i] = true;
                    break;
                }
            }
        }
        return canReach[0];
    }
}
```

Greedy

```java
class Solution {
    public boolean canJump(int[] nums) {
        int n = nums.length;
        int goodId = n - 1;
        for (int i = n - 2; i >=0 ; i--) {
            if (nums[i] + i >= goodId) goodId = i;
        }
        return goodId == 0;
    }
}
```

### Additional {#additional}



