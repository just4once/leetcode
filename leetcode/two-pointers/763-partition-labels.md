# 763-partition-labels

## Question {#question}

[https://leetcode.com/problems/partition-labels/description/](https://leetcode.com/problems/partition-labels/description/)

A string S of lowercase letters is given. We want to partition this string into as many parts as possible so that each letter appears in at most one part, and return a list of integers representing the size of these parts.

**Example:**

```text
Input: S = "ababcbacadefegdehijhklij"
Output: [9,7,8]
Explanation:
The partition is "ababcbaca", "defegde", "hijhklij".
This is a partition so that each letter appears in at most one part.
A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits S into less parts.
```

**Note:**

1. S will have length in range \[1, 500\].
2. S will consist of lowercase letters \('a' to 'z'\) only.

## Thought Process {#thought-process}

1. Two Pointers
   1. For each character, we need to find the rightest index for it, then within this range, we need to further expand the right boundary
   2. Use map to facilitate the search rightest index and also use two pointers to find the length
   3. Time complexity O\(n\)
   4. Space complexity O\(128\) or O\(1\)

## Solution

```java
class Solution {
    public List<Integer> partitionLabels(String S) {
        int[] map = new int[128];
        char[] chars = S.toCharArray();
        for (int i = 0; i < chars.length; i++) map[chars[i]] = i;
        int left = 0, right = 0;
        List<Integer> res = new ArrayList<>();
        while (left < chars.length) {
            right = map[chars[left]];
            for (int i = left; i < right; i++) right = Math.max(right, map[chars[i]]);
            res.add(right - left + 1);
            left = right + 1;
        }
        return res;
    }
}
```

## Additional {#additional}

