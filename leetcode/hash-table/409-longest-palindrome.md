# 409-longest-palindrome

## Question {#question}

[https://leetcode.com/problems/longest-palindrome/description/](https://leetcode.com/problems/longest-palindrome/description/)

Given a string which consists of lowercase or uppercase letters, find the length of the longest palindromes that can be built with those letters.

This is case sensitive, for example "Aa" is not considered a palindrome here.

 **Note:** 

Assume the length of given string will not exceed 1,010.

**Example:**

```text
Input:
"abccccdd"

Output:
7

Explanation:
One longest palindrome that can be built is "dccaccd", whose length is 7.
```

## Thought Process {#thought-process}

1. Hash Table
   1. Use hash table to record the count for all characters, we will want to use all the even count for character and plus 1 if any one of them has odd count
   2. Time complexity O\(n\)
   3. Space complexity O\(n\) or O\(1\)

## Solution

```java
class Solution {
    public int longestPalindrome(String s) {
        if (s == null) return 0;
        if (s.length() <= 1) return s.length();
        Map<Character, Integer> map = new HashMap<>();
        for (char c : s.toCharArray()) {
            map.put(c, map.getOrDefault(c, 0) + 1);
        }
        int res = 0;
        Iterator<Map.Entry<Character, Integer>> iter = map.entrySet().iterator();
        while (iter.hasNext()) {
            Map.Entry<Character, Integer> next = iter.next();
            if (next.getValue() % 2 == 0) {
                res += next.getValue();
                iter.remove();
            } else {
                res += next.getValue() - 1;
            }
        }
        return map.isEmpty() ? res : res + 1;
    }
}
```

```java
class Solution {
    public int longestPalindrome(String s) {
        if (s == null) return 0;
        if (s.length() <= 1) return s.length();
        int[] map = new int[128];
        for (char c : s.toCharArray()) {
            map[c]++;
        }
        boolean isOdd = false;
        int res = 0;
        for (char c = 'a'; c <= 'z'; c++) {
            res += map[c]/2;
            if (map[c] % 2 == 1) isOdd = true; 
        }
        for (char c = 'A'; c <= 'Z'; c++) {
            res += map[c]/2;
            if (map[c] % 2 == 1) isOdd = true; 
        }
        return isOdd ? res * 2 + 1 : res * 2;
    }
}
```

## Additional {#additional}

