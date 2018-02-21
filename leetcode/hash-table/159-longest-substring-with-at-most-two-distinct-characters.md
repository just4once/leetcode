### Question {#question}

[https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/description/](https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/description/)

Given a string, find the length of the longest substring T that contains at most 2 distinct characters.

**Example:**

```
Given s = “eceba”,

T is "ece" which its length is 3.
```

### Thought Process {#thought-process}

1. Hash Table - extensible to K characters
   1. Use map to store the position
   2. When the map exceed the requirement, we reset by removing the character has left most index
   3. Time complexity O\(kn\)
   4. Time complexity O\(n\)
2. Hash Table - time optimized
   1. Know the other character to retried the index
   2. Use XOR to save the two character, once we reach the map size of 2, we can retried the other character by XOR with previous character
   3. Time complexity O\(n\)
   4. Space complexity O\(n\)
3. Typical Template

### Solution

```java
class Solution {
    public int lengthOfLongestSubstringTwoDistinct(String s) {
        if (s.length() <= 2) return s.length();
        char[] chars = s.toCharArray();
        Map<Character, Integer> map = new HashMap<>();
        int left = 0, right = 0, n = s.length();
        int res = 0, k = 2;
        char pre = chars[left];
        while (right < n) {
            if (map.size() == k && !map.containsKey(chars[right])) {
                int leftMost = n;
                for (int index : map.values()) {
                    leftMost = Math.min(index, leftMost);
                }
                map.remove(chars[leftMost - 1]);
                left = leftMost;
            }
            map.put(chars[right++], right);
            res= Math.max(right - left, res);
        }
        return res;
    }
}
```

```java
class Solution {
    public int lengthOfLongestSubstringTwoDistinct(String s) {
        if (s.length() <= 2) return s.length();
        char[] chars = s.toCharArray();
        Map<Character, Integer> map = new HashMap<>();
        int left = 0, right = 1, n = s.length();
        int res = 1, unique = 1;
        char pre = chars[left];
        map.put(pre, 1);
        while (right < n) {
            if (map.size() == 2 && !map.containsKey(chars[right])) {
                pre ^= chars[right - 1];
                unique = 1;
                left = map.get(pre);
                map.remove(pre);
                pre = chars[right - 1];
            }
            if (chars[right] != chars[right - 1] && unique == 1) {
                pre ^= chars[right];
                unique++;
            }
            map.put(chars[right++], right);
            res= Math.max(right - left, res);
        }
        return res;
    }
}
```

```java
class Solution {
    public int lengthOfLongestSubstringTwoDistinct(String s) {
        if (s.length() <= 2) return s.length();
        char[] chars = s.toCharArray();
        int left = 0, right = 0, n = s.length();
        int res = 0, unique = 0;
        int[] map = new int[128];
        while (right < n) {
            if (map[chars[right++]]++ == 0) {
                unique++;
            }
            while (unique > 2) {
                if (map[chars[left++]]-- == 1) unique--;
            }
            res = Math.max(res, right - left);
        }
        return res;
    }
}
```

### Additional {#additional}



