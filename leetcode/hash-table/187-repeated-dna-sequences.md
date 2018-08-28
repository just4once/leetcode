# 187-repeated-dna-sequences

## Question {#question}

[https://leetcode.com/problems/repeated-dna-sequences/description/](https://leetcode.com/problems/repeated-dna-sequences/description/)

All DNA is composed of a series of nucleotides abbreviated as A, C, G, and T, for example: "ACGAATTCCG". When studying DNA, it is sometimes useful to identify repeated sequences within the DNA.

Write a function to find all the 10-letter-long sequences \(substrings\) that occur more than once in a DNA molecule.

**Example:**

```text
Given s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT",

Return:
["AAAAACCCCC", "CCCCCAAAAA"].
```

## Thought Process {#thought-process}

1. Brute Force - Two Sets
   1. Simply cut the string at different position to create length 10 substring
   2. If we can still add to the first set that means we encounter if for the first time, otherwise we can we can add it to the second set
   3. Time complexity O\(n\)
   4. Space complexity O\(n\)
2. Rolling Hash
   1. Because we have only four letters, we can represent it with two bits, meaning 0, 1, 2, 3 for A, C, G, and T
   2. Every time we see a letter we shift the hash leftward by two bits
   3. When we finish hashing the 10th letter, we need to mindful about clear the bits at the front from previous hashing
   4. Time complexity O\(n\)
   5. Space complexity O\(n\)

## Solution

```java
class Solution {
    public List<String> findRepeatedDnaSequences(String s) {
        List<String> res = new ArrayList<>();
        if (s.length() <= 10) return res;
        Set<String> one = new HashSet<>(), two = new HashSet<>();
        int n = s.length();
        for (int i = 0; i <= n - 10; i++) {
            String sub = s.substring(i, i + 10);
            if (!one.add(sub)) two.add(sub);
        }
        res.addAll(two);
        return res;
    }
}
```

```java
class Solution {
    public List<String> findRepeatedDnaSequences(String s) {
        List<String> res = new ArrayList<>();
        if (s.length() <= 10) return res;
        Set<String> saved = new HashSet<>();
        Set<Integer> set = new HashSet<>();
        Map<Character, Integer> map = new HashMap<>();
        map.put('A', 0);
        map.put('C', 1);
        map.put('G', 2);
        map.put('T', 3);
        int n = s.length();
        int hash = 0;
        char[] chars = s.toCharArray();
        for (int i = 0; i < 9; i++) {
            hash <<= 2;
            hash |= map.get(chars[i]);
        }
        for (int i = 9; i < n; i++) {
            hash <<= 2;
            hash |= map.get(chars[i]);
            // clear the bit before 20 bits
            hash &= 0xfffff;
            if (!set.add(hash)) saved.add(String.valueOf(chars, i - 9, 10));
        }
        res.addAll(saved);
        return res;
    }
}
```

## Additional {#additional}

