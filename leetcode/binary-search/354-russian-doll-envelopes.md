### Question {#question}

[https://leetcode.com/problems/russian-doll-envelopes/description/](https://leetcode.com/problems/russian-doll-envelopes/description/)

You have a number of envelopes with widths and heights given as a pair of integers \(w, h\). One envelope can fit into another if and only if both the width and height of one envelope is greater than the width and height of the other envelope.

What is the maximum number of envelopes can you Russian doll? \(put one inside other\)

**Example:**

```
Given envelopes = [[5,4],[6,4],[6,7],[2,3]],
the maximum number of envelopes you can Russian doll is 3 ([2,3] => [5,4] => [6,7]).
```

### Thought Process {#thought-process}

1. DP
   1. Using dp\[i\] to store the max number ending at envelope i
   2. We need to sort the element based on their width, w
   3. Then for each envelope before envelope i, we try to see if it can be placed inside envelope i
   4. Time complexity O\(n^2\)
   5. Space complexity O\(n\)
2. Binary Search

### Solution

```java

```

### Additional {#additional}



