### Question {#question}

[https://leetcode.com/problems/shortest-palindrome/description/](https://leetcode.com/problems/shortest-palindrome/description/)

Given a string S, you are allowed to convert it to a palindrome by adding characters in front of it. Find and return the shortest palindrome you can find by performing this transformation.

**Example:**

```
Given "aacecaaa", return "aaacecaaa".

Given "abcd", return "dcbabcd".
```

### Thought Process {#thought-process}

1. Expand and Reach the End
   1. For each character or character pair, we try to use it as palindromic center
   2. Our goal is to reach the front end, because failing to do so, we need to revert to using the first character or character pair or return 0 from expand function
   3. Then the answer is simply n - len + n
   4. Time complexity O\(n^2\)
   5. Space complexity O\(1\)  
2. KMP
   1. KMP explains here, [https://blog.csdn.net/v\_july\_v/article/details/7041827](https://blog.csdn.net/v_july_v/article/details/7041827)
   2. Building Partial Table, [http://jakeboxer.com/blog/2009/12/13/the-knuth-morris-pratt-algorithm-in-my-own-words/](http://jakeboxer.com/blog/2009/12/13/the-knuth-morris-pratt-algorithm-in-my-own-words/)
   3. 

### Solution

```java
class Solution {
    public String shortestPalindrome(String s) {
        if (s.length() <= 1) return s;
        char[] chars = s.toCharArray();
        int n = s.length(), len = 1;
        for (int i = 1; i <= n / 2; i++) {
            len = Math.max(len, expand(chars, i - 1, i));
            len = Math.max(len, expand(chars, i, i));
        }
        StringBuilder sb = new StringBuilder();
        for (int i = n - 1; i >= len; i--) sb.append(chars[i]);
        sb.append(s);
        return sb.toString();
    }
    
    private int expand(char[] chars, int i, int j) {
        while (i >= 0 && j < chars.length && chars[i] == chars[j]) {
            i--;
            j++;
        }
        return i == -1 ? j - i - 1 : 0;
    }
}
```

### Additional {#additional}



