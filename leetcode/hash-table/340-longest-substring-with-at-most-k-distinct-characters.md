### Question {#question}

[https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/description/](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/description/)

Given a string, find the length of the longest substring T that contains at most k distinct characters.

**Example:**

```
Given s = “eceba” and k = 2,
T is "ece" which its length is 3.
```

### Thought Process {#thought-process}

1. Sliding Window
   1. The map track the count of each character, if this character is seen the first time, we increase the counter for unique character
   2. Left and right pointers to track the current window
   3. Time complexity O\(n\)
   4. Space complexity O\(n\) or O\(1\)
2. Sliding Window - Hash Map to Index
   1. Pretty similar idea live above, where we save the index of next character
   2. Time complexity O\(n\)
   3. Space complexity O\(1\)

### Solution

```java
class Solution {
    public int lengthOfLongestSubstringKDistinct(String s, int k) {
        int[] map = new int[128];
        char[] chars = s.toCharArray();
        int left = 0, right = 0;
        int max = 0, n = s.length();
        int count = 0;
        while (right < n) {
            if (map[chars[right++]]++ == 0) {
                count++;
                while (count > k) {
                    if (--map[chars[left++]] == 0) count--;
                }
            }
            max = Math.max(max, right - left);
        }
        return max;
    }
}
```

```java
class Solution {
    public int lengthOfLongestSubstringKDistinct(String s, int k) {
        if (k == 0) return 0;
        Map<Character, Integer> map = new HashMap<>();
        char[] chars = s.toCharArray();
        int left = 0, right = 0;
        int max = 0, n = s.length();
        int count = 0;
        while (right < n) {
            map.put(chars[right], right);
            if (map.size() > k) {
                int leftMost = Integer.MAX_VALUE;
                for (int id : map.values()) {
                    leftMost = Math.min(leftMost, id);
                }
                map.remove(chars[leftMost]);
                left = leftMost + 1;
            }
            right++;
            max = Math.max(max, right - left);
        }
        return max;
    }
}
```

### Additional {#additional}



