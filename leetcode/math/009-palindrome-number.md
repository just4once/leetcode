### Question {#question}

[https://leetcode.com/problems/palindrome-number/description/](https://leetcode.com/problems/palindrome-number/description/)

Determine whether an integer is a palindrome. Do this without extra space.

**Example:**

```

```

### Thought Process {#thought-process}

1. Revert Half
   1. Create the reverse of right half of the number
   2. Check the equivalence of x and its reverse or x and its reverse / 10
   3. Time complexity O\(log n\)
   4. Space complexity O\(1\)

### Solution

```java
class Solution {
    public boolean isPalindrome(int x) {
        if(x < 0 || (x != 0 && x % 10 == 0)) return false;
        int rev = 0;
        while (x > rev) {
            rev = rev * 10 + x % 10;
            x /= 10;
        }
        return x == rev || x == rev / 10;
    }
}
```

### Additional {#additional}



