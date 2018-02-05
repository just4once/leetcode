### Question {#question}

Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

**Example:**

```
Given array A = [2,3,1,1,4]

The minimum number of jumps to reach the last index is 2. (Jump 1 step from index 0 to 1, then 3 steps to the last index.)
```

### Thought Process {#thought-process}

1. Top down recursion
   1. Recursion to find the minimum step for each of step we took
   2. To avoid repeatedly doing the same work, we cache the minimum step in the memo
   3. Unfortunately, this solution yield stack overflow for the input of 1's where the length exceed the depth of recursion in Java
   4. Time complexity O\(n\)
   5. Space complexity O\(log n\)
2. Bottom up
   1. We do the reverse way, we start from the last index
   2. Then for each element before the last, we loop through all the step possible and find the minimum step
   3. Unfortunately, this solution yield stack overflow for case where each number is great and every loop is long
   4. Time complexity O\(n\)
   5. Space complexity O\(n\)
3. Greedy
   1. Observe that every we have a choice to jump, we need to maximize our distance travel
   2. Similar to BFS, each jumps cover a range of cell, we have to find the furthest point we can travel
   3. Then from the next cell to the further point, we repeat the same process again until we reach the end

### Solution

Top down \(Stack Overflow\)

```java
class Solution {
    public int jump(int[] nums) {
        int[] memo = new int[nums.length];
        jump(nums, memo, 0);
        return memo[0];
    }
    
    public int jump(int[] nums, int[] memo, int id) {
        if (id == nums.length - 1) return 0;
        if (memo[id] != 0) return memo[id];
        int step = Integer.MAX_VALUE;
        for (int i = 1; i <= nums[id] && id + i < nums.length; i++) {
            step = Math.min(step, jump(nums, memo, id + i) + 1);
        }
        memo[id] = step;
        return step;
    }
}
```

Bottom up \(Stack Overflow\)

```java
class Solution {
    public int jump(int[] nums) {
        int n = nums.length;
        Integer[] memo = new Integer[n];
        memo[n - 1] = 0;
        for (int i = n - 2; i >= 0; i--) {
            int min = Integer.MAX_VALUE;
            for (int step = nums[i]; step >= 1; step--) {
                int next = i + step;
                if (next >= n - 1) {
                    memo[i] = 1;
                    break;
                }
                if (memo[next] != null && memo[next] < min) {
                    min = memo[next];
                    memo[i] = min + 1;
                }
            }
        }
        return memo[0];
    }
}
```

Greedy \(BFS\)

```java
class Solution {
    public int jump(int[] nums) {
        int end = 0, maxEnd = 0, n = nums.length, jump = 0;
        while (maxEnd < n - 1) {
            int tmp = 0;
            // loop through all the choice and see how far we can reach 
            // next round
            for (int i = end; i <= maxEnd; i++) {
                tmp = Math.max(tmp, nums[i] + i);
            }
            jump++;
            end++;
            maxEnd = tmp;
        }
        return jump;
    }
}
```

Greedy 2

```java
class Solution {
    public int jump(int[] nums) {
        int jump = 0, maxEnd = 0, nextEnd = 0;
        // skip the last position
        for (int i = 0; i < nums.length - 1; i++) {
            // we keep searching the furthest point we can reach
            nextEnd = Math.max(nextEnd, nums[i] + i);
            // once we are at the end point, we have used up all
            // our choice, and it's time to jump again
            if (i == maxEnd) {
                jump++;
                maxEnd = nextEnd;
            }
        }
        return jump;
    }
}
```

### Additional {#additional}



