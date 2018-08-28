# 136-single-number

## Question {#question}

[https://leetcode.com/problems/single-number/description/](https://leetcode.com/problems/single-number/description/)

Given an array of integers, every element appears twice except for one. Find that single one.

**Example:**

```text

```

## Thought Process {#thought-process}

1. Hash Table
   1. Use set to record the number, if we encounter the number again, we remove them, in the end there will be only 1 number left
   2. Time complexity O\(n\)
   3. Space complexity O\(n\)
2. XOR
   1. Use the bit trick where xor a number twice cancel the number one
   2. Time complexity O\(n\)
   3. Space complexity O\(1\)

## Solution

```java
class Solution {
    public int singleNumber(int[] nums) {
        Set<Integer> set = new HashSet<>();
        for (int num : nums){
            if (!set.contains(num)) set.add(num);
            else set.remove(num);
        }
        return (int) set.iterator().next();
    }
}
```

```java
class Solution {
    public int singleNumber(int[] nums) {
        int res = 0;
        for (int num : nums){
            res ^= num;
        }
        return res;
    }
}
```

## Additional {#additional}

