# 368-largest-divisible-subset

## Question {#question}

[https://leetcode.com/problems/largest-divisible-subset/description/](https://leetcode.com/problems/largest-divisible-subset/description/)

Given a set of distinct positive integers, find the largest subset such that every pair \(Si, Sj\) of elements in this subset satisfies: Si % Sj = 0 or Sj % Si = 0.

If there are multiple solutions, return any subset is fine.

**Example:**

```text
nums: [1,2,3]

Result: [1,2] (of course, [1,3] will also be ok)
```

```text
nums: [1,2,4,8]

Result: [1,2,4,8]
```

## Thought Process {#thought-process}

1. Parent Array and Count Array
   1. Use parent array to keep track of each number's parent, and count array to keep track of the length of sequence ending on current number
   2. Time complexity O\(n^2\)
   3. Space complexity O\(n\)

## Solution

```java
class Solution {
    public List<Integer> largestDivisibleSubset(int[] nums) {
        Arrays.sort(nums);
        int n = nums.length;
        int[] count = new int[n], pre = new int[n];
        int max = 0, index = -1;
        for (int i = 0; i < n; i++) {
            count[i] = 1;
            pre[i] = -1;
            for (int j = i - 1; j >= 0; j--) {
                if (nums[i] % nums[j] == 0 && 1 + count[j] > count[i]) {
                    count[i] = count[j] + 1;
                    pre[i] = j;
                }
            }
            if (count[i] > max) {
                max = count[i];
                index = i;
            }
        }
        LinkedList<Integer> list = new LinkedList<>();
        while (index != -1) {
            list.addFirst(nums[index]);
            index = pre[index];
        }
        return list;
    }
}
```

## Additional {#additional}

