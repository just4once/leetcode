### Question {#question}

[https://leetcode.com/problems/palindrome-permutation/description/](https://leetcode.com/problems/palindrome-permutation/description/)

Given a string, determine if a permutation of the string could form a palindrome.

**Example:**

```
"code" -> False, "aab" -> True, "carerac" -> True.
```

### Thought Process {#thought-process}

1. Hash Table - Two passes
   1. Use map to store the frequency of character, if we have seen odd frequency more than once, we can't make a permutation that is palindrom
   2. Time complexity O\(n\)
   3. Space complexity O\(n\)
2. Hash Table - One pass 

### Solution

```java
class Solution {
    public boolean canPermutePalindrome(String s) {
        if (s.length() <= 1) return true;
        int[] map = new int[128];
        char[] chars = s.toCharArray();
        for (char c : chars) map[c]++;
        boolean oddSeen = false;
        for (char a = 0; a < 128; a++) {
            if (map[a] % 2 == 1) {
                if (oddSeen) return false;
                oddSeen = true;
            }
        }
        return true;
    }
}
```

```java
class Solution {
    public boolean canPermutePalindrome(String s) {
        if (s.length() <= 1) return true;
        int[] map = new int[128];
        int oddCnt = 0;
        for (char c : s.toCharArray()) {
            map[c]++;
            if (map[c] % 2 == 1) oddCnt++;
            else oddCnt--;
        }
        return oddCnt <= 1 ? true : false;
    }
}
```

### Additional {#additional}



