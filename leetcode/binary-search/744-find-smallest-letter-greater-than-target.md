### Question {#question}

[https://leetcode.com/problems/find-smallest-letter-greater-than-target/description/](https://leetcode.com/problems/find-smallest-letter-greater-than-target/description/)

Given a list of sorted characters letters containing only lowercase letters, and given a target letter target, find the smallest element in the list that is larger than the given target.

Letters also wrap around. For example, if the target is target = 'z' and letters = \['a', 'b'\], the answer is 'a'.

**Example:**

```
Input:
letters = ["c", "f", "j"]
target = "a"
Output: "c"

Input:
letters = ["c", "f", "j"]
target = "c"
Output: "f"

Input:
letters = ["c", "f", "j"]
target = "d"
Output: "f"

Input:
letters = ["c", "f", "j"]
target = "g"
Output: "j"

Input:
letters = ["c", "f", "j"]
target = "j"
Output: "c"

Input:
letters = ["c", "f", "j"]
target = "k"
Output: "c"
```

**Note:**

1. letters has a length in range \[2, 10000\].
2. letters consists of lowercase letters, and contains at least 2 unique letters.
3. target is a lowercase letter.

### Thought Process {#thought-process}

1. Binary Search
   1. We add 1 to target and mod 26 to get the "right" target
   2. If the index is equal to the length of list, we return the first element
   3. Time complexity O\(logn\)
   4. Space complexity O\(1\)
2. asd

### Solution

```java
class Solution {
    public char nextGreatestLetter(char[] letters, char target) {
        target = (char) ((target + 1 - 'a') % 26 + 'a');
        int i = Arrays.binarySearch(letters, target);
        if (i < 0) i = -(i + 1);
        if (i == letters.length) i = 0;
        return letters[i];
    }
}
```

### Additional {#additional}



