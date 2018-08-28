# 066-plus-one

## Question {#question}

[https://leetcode.com/problems/plus-one/description/](https://leetcode.com/problems/plus-one/description/)

Given a non-negative integer represented as a **non-empty** array of digits, plus one to the integer.

You may assume the integer do not contain any leading zero, except the number 0 itself.

The digits are stored such that the most significant digit is at the head of the list.

**Example:**

```text

```

## Thought Process {#thought-process}

1. Since the most significant digit is at the head, we need to go from back of the array
2. We can break fast if the current digit is smaller than 9, since adding one won't impact the rest front digit
3. Otherwise, we need to keep going forward
4. If we are able to reach to the head of the array, and still not returning, there is only one possibility that all digits are 9's, then we would need to create an array with number of digit + 1 and the first digit is 1
5. Time complexity O\(n\)
6. Space complexity O\(1\) or O\(n\) when all digits are 9

## Solution

```java
class Solution {
    public int[] plusOne(int[] digits) {
        for(int i = digits.length - 1; i >= 0; i--){
            if (digits[i]++ < 9) return digits;
            digits[i] = 0;
        }
        int[] result = new int[digits.length + 1];
        result[0] = 1;
        return result;
    }
}
```

## Additional {#additional}

