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
   1. The goal is to find the longest palindrome starting from first character
   2. So we try to expand each character as palindromic center
   3. After finding the length, then the answer is simply n - len + n
   4. Time complexity O\(n^2\)
   5. Space complexity O\(1\)  
2. KMP
   1. KMP explains here, [https://blog.csdn.net/v\_july\_v/article/details/7041827](https://blog.csdn.net/v_july_v/article/details/7041827)
   2. Building Partial Table, [http://jakeboxer.com/blog/2009/12/13/the-knuth-morris-pratt-algorithm-in-my-own-words/](http://jakeboxer.com/blog/2009/12/13/the-knuth-morris-pratt-algorithm-in-my-own-words/)
   3. Using KMP table can help us determine the longest palindrome from first character
   4. The trick is use s + "\#" + reverse\(s\), and the last cell of the table will be the length
   5. The match of proper prefix of s and proper suffix of reverse s indicates the that has to be a palindrome
   6. Time complexity O\(n\)
   7. Space complexity O\(n\) 
3. Manacger
   1. asdasd
   2. 

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

```java
class Solution {
    public String shortestPalindrome(String s) {
        String rev = reverse(s);
        int n = s.length();
        int len = kmp(s + "#" + rev);
        return rev.substring(0, n - len) + s;
    }
    
    private String reverse(String s) {
        StringBuilder sb = new StringBuilder(s);
        return sb.reverse().toString();
    }
    
    private int kmp(String s) {
        int n = s.length(), i = 0;
        int[] table = new int[n];
        char[] chars = s.toCharArray();
        for (int j = 1; j < n; j++) {
            while (i > 0 && chars[i] != chars[j]) i = table[i - 1];
            if (chars[i] == chars[j]) i++;
            table[j] = i;
        }
        return table[n - 1];
    }
}
```

### Additional {#additional}



