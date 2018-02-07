### Question {#question}

Given an array withnobjects colored red, white or blue, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

**Follow up:**  
A rather straight forward solution is a two-pass algorithm using counting sort.  
First, iterate the array counting number of 0's, 1's, and 2's, then overwrite array with total number of 0's, then 1's and followed by 2's.

Could you come up with an one-pass algorithm using only constant space?

**Example:**

```

```

### Thought Process {#thought-process}

1. Counting sort - Two passes
   1. We can count the number of each color and fill the array
   2. Time complexity O\(n\)
   3. Space complexity O\(1\)
2. In place - One pass
   1. Two pointers to track the index of 0 and 2, the index of color red and color blue
   2. Whenever we encounter these two color we swap them to the end
   3. Continue until these two pointers meet
   4. Time complexity O\(n\)
   5. Space complexity O\(1\)

### Solution

```java
class Solution {
    public void sortColors(int[] nums) {
        int redCount = 0, whiteCount = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == 0) redCount++;
            else if (nums[i] == 1) whiteCount++;
        }
        // fill the color red, 0, until redCount
        for (int i = 0; i < redCount; i++) nums[i] = 0;
        // fill the color white, 1, until redCount + whiteCount
        for (int i = redCount; i < redCount + whiteCount; i++) nums[i] = 1;
        // fill the color blue, 2, until the end
        for (int i = redCount + whiteCount; i < nums.length; i++) nums[i] = 2;
    }
}
```

```java
class Solution {
    public void sortColors(int[] nums) {
        int id0 = 0, id2 = nums.length - 1;
        int i = 0;
        while (i <= id2) {
            if (nums[i] == 0) {
                // when 0 swap with id0 it must have been an 1, because any 2 exist
                // before will be at the end of array
                nums[i] = nums[id0];
                nums[id0++] = 0;
            } else if (nums[i] == 2) {
                // to reset against i++ below, whatever go swap to the ith position
                // we need to redetermine where it should fall
                nums[i--] = nums[id2];
                nums[id2--] = 2;
            }
            i++;
        }
    }
}
```

### Additional {#additional}



