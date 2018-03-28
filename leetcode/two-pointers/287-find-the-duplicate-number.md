### Question {#question}

[https://leetcode.com/problems/find-the-duplicate-number/description/](https://leetcode.com/problems/find-the-duplicate-number/description/)

Given an array nums containing n + 1 integers where each integer is between 1 and n \(inclusive\), prove that at least one duplicate number must exist. Assume that there is only one duplicate number, find the duplicate one.

**Example:**

```

```

### Thought Process {#thought-process}

1. Two Pointers and Mid Element
   1. Use the mid as way to count the number that is smaller than it
   2. If count is greater than mi, the number is on the smaller side, otherwise is on the high side
   3. Time complexity O\(n^2\)
   4. Space complexity O\(1\)
2. Sort \(Violate the Requirement\)
   1. Time complexity O\(nlogn\)
   2. Space complexity O\(1\)
3. Hash Table \(Violate the Requirement\)
   1. Time complexity O\(n\)
   2. Space complexity O\(n\)
4. Floyd's Tortoise and Hare
   1. We can treat this as linked list while every value in the array is the index
   2. 

### Solution

```java
class Solution {
    public int findDuplicate(int[] nums) {
        int lo = 1, hi = nums.length - 1, mi, count;
        while (lo < hi) {
            mi = lo + (hi - lo)/2;
            count = 0;
            for (int num : nums) {
                if (num <= mi) count++;
            }
            if (count > mi) hi = mi;
            else lo = mi + 1;
        }
        return lo;
    }
}
```

```java
class Solution {
    public int findDuplicate(int[] nums) {
        Arrays.sort(nums);
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] == nums[i-1]) {
                return nums[i];
            }
        }
        return -1;
    }
}
```

```java
class Solution {
    public int findDuplicate(int[] nums) {
        Set<Integer> seen = new HashSet<Integer>();
        for (int num : nums) {
            if (!seen.add(num)) return num;
        }
        return -1;
    }
}
```

```java
class Solution {
    public int findDuplicate(int[] nums) {
        int slow = nums[0], fast = nums[0];
        do {
            slow = nums[slow];
            fast = nums[nums[fast]];
        } while (slow != fast);
        // reset fast and travel to the entry of circle
        fast = nums[0];
        while (slow != fast) {
            slow = nums[slow];
            fast = nums[fast];
        }
        return slow;
    }
}
```

### Additional {#additional}



