### Question {#question}

[https://leetcode.com/problems/first-missing-positive/description/](https://leetcode.com/problems/first-missing-positive/description/)

Given an unsorted integer array, find the first missing positive integer.

Your algorithm should run in O\(n\) time and uses constant space.

**Example:**

```
Given [1,2,0] return 3,
and [3,4,-1,1] return 2.
```

### Thought Process {#thought-process}

1. The restriction means what we cannot use any kind of cache, therefore we should do thing in place.
2. As we go through the array, we put the element in the correct spot at \(num - 1\) index
3. In the second pass, if the ith index is not equal to i + 1, we know this is the first missing positive

### Solution

```java
class Solution {
    public int firstMissingPositive(int[] nums) {
        int i = 0;
        while (i < nums.length) {
            if (nums[i] > 0 && nums[i] <= nums.length && nums[nums[i] - 1] != nums[i]) {
                swap(nums, nums[i] - 1, i);
            } else {
                i++;
            }
        }
        i = 0;
        while (i < nums.length) {
            if (nums[i] != i + 1) return i + 1;
            i++;
        }
        return nums.length + 1;
    }
    
    public void swap(int[] nums, int i, int j){
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
}
```

### Additional {#additional}



