### Question {#question}

[https://leetcode.com/problems/rearrange-string-k-distance-apart/description/](https://leetcode.com/problems/rearrange-string-k-distance-apart/description/)

Given a non-empty string **s** and an integer **k**, rearrange the string such that the same characters are at least distance k from each other.

All input strings are given in lowercase letters. If it is not possible to rearrange the string, return an empty string "".

**Example:**

```
s = "aabbcc", k = 3

Result: "abcabc"

The same letters are at least distance 3 from each other.
```

```
s = "aaabc", k = 3 

Answer: ""

It is not possible to rearrange the string.
```

```
s = "aaadbbcc", k = 2

Answer: "abacabcd"

Another possible answer is: "abcabcda"

The same letters are at least distance 2 from each other.
```

### Thought Process {#thought-process}

1. Map and MaxHeap
   1. Use map to record the count for each character, and use heap to poll the character with most count
   2. Every time we poll a character out and append this character to our string builder and save the character to a queue for latter use
   3. Time complexity O\(n log\(26\)\) or O\(n\)
   4. Space complexity O\(1\)
2. Map and Index Map
   1. We store the count and valid index for each letter
   2. Every time we insert a character to our result, we need to increase this character next valid position to i + k
   3. We use a separate function to search the next character from 26 letters, where it has maximum count and it falls outside the valid index
   4. Time complexity O\(n\)
   5. Space complexity O\(1\)

### Solution

```java
class Solution {
    public String rearrangeString(String s, int k) {
        Map<Character, Integer> map = new HashMap<>();
        for (char c : s.toCharArray()) {
            map.put(c, map.getOrDefault(c, 0) + 1);
        }
        PriorityQueue<Map.Entry<Character, Integer>> maxHeap = new PriorityQueue<>((a, b) -> b.getValue() - a.getValue());
        maxHeap.addAll(map.entrySet());
        StringBuilder sb = new StringBuilder();
        Queue<Map.Entry<Character, Integer>> wait = new LinkedList<>();
        while (!maxHeap.isEmpty()) {
            Map.Entry<Character, Integer> cur = maxHeap.poll();
            sb.append(cur.getKey());
            cur.setValue(cur.getValue() - 1);
            wait.offer(cur);
            if (wait.size() < k) continue;
            Map.Entry<Character, Integer> next = wait.poll();
            if (next.getValue() > 0) maxHeap.offer(next);
        }
        return sb.length() == s.length() ? sb.toString() : "";
    }
}
```

```
sad
```

### Additional {#additional}



