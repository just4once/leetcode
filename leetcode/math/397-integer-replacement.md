### Question {#question}

[https://leetcode.com/problems/integer-replacement/description/](https://leetcode.com/problems/integer-replacement/description/)

Given a positive integer n and you can do operations as follow:

1. If n is even, replace n with n/2.
2. If n is odd, you can replace n with either n + 1 or n - 1.

What is the minimum number of replacements needed for n to become 1?

**Example:**

```
Input:
8

Output:
3

Explanation:
8 -> 4 -> 2 -> 1
```

```
Input:
7

Output:
4

Explanation:
7 -> 8 -> 4 -> 2 -> 1
or
7 -> 6 -> 3 -> 2 -> 1
```

### Thought Process {#thought-process}

1. Pattern Finding
   1. Three cases
      1. If n is even, we just follow the rule
      2. If n is odd we need to look at the second last digit, if it is 1, adding 1 will be able to remove two 1s, otherwise we can just decrement it
      3. One exception is 3, which we should decrement by 1
   2. Time complexity O\(log n\)
   3. Space complexity O\(1\)

### Solution

```java
class Solution {
    public int integerReplacement(int n) {
        int count = 0;
        while (n != 1) {
            count++;
            if (n % 2 == 0) n >>>= 1;
            else if (n == 3 || ((n >>> 1) & 1) == 0) n -= 1;
            else n += 1;
        }
        return count;
    }
}
```

### Additional {#additional}



