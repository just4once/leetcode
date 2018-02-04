### Question {#question}

[https://leetcode.com/problems/next-permutation/description/](https://leetcode.com/problems/next-permutation/description/)

Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order \(ie, sorted in ascending order\).

The replacement must be in-place, do not allocate extra memory.

**Example:**

```
1,2,3 → 1,3,2
3,2,1 → 1,2,3
1,1,5 → 1,5,1
```

### Thought Process {#thought-process}

1. Since we want the next greater number, we better scan from the back toward the front
2. When we find an element that is smaller than its right element\(s\) we know this location needs to be updated with a greater element, let's called this index i
3. However, we don't want any element that is greater. We want an element that is smallest among all the potential candidates.
4. To find that, we again scan from the back and locate that element and swap with index i
5. Now, all we have to make the remaining elements in ascending order by reversing
6. Time complexity O\(n\)
7. Space complexity O\(1\)

### Solution

```java
class Solution {
    public void nextPermutation(int[] nums) {
        int i = nums.length - 2;
        while (i >= 0 && nums[i] >= nums[i+1]) i--;
        if (i >= 0){
            int j = nums.length - 1;
            while(j >= 0 && nums[j] <= nums[i]) j--;
            swap(nums, i, j);
        }
        reverse(nums, i + 1);
    }

    public void swap(int[] nums, int i, int j){
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }

    public void reverse(int[] nums, int start){
        int end = nums.length -1;
        while(start < end){
            swap(nums, start++, end--);
        }
    }
}
```

### Additional {#additional}



