### Question {#question}

[https://leetcode.com/problems/strobogrammatic-number/description/](https://leetcode.com/problems/strobogrammatic-number/description/)

A strobogrammatic number is a number that looks the same when rotated 180 degrees \(looked at upside down\).

Write a function to determine if a number is strobogrammatic. The number is represented as a string.

**Example:**

```
The numbers "69", "88", and "818" are all strobogrammatic.
```

### Thought Process {#thought-process}

1. Hash Table
   1. Put characters and their respective strobogrammatic pair in the map as key and value pair
   2. We can treat this as palindrome problem, where we have two pointers at the start and end
   3. Time complexity O\(n\)
   4. Space complexity O\(1\), since we only put 5 key-value pairs
2. String contains
   1. We can leverage the fact that there is only 5 only pairs, 00 11 88 69 96, where we repeatedly search if char\[left\] +  char\[right\] concatenation is contained in the pairs
   2. Time complexity O\(14 \* n/2\) -&gt; O\(n\)
   3. Space complexity O\(1\)

### Solution

```java
class Solution {
    public boolean isStrobogrammatic(String num) {
        Map<Character, Character> map = new HashMap<>();
        map.put('0', '0');
        map.put('1', '1');
        map.put('6', '9');
        map.put('8', '8');
        map.put('9', '6');
        int left = 0, right = num.length() - 1;
        char[] n = num.toCharArray();
        while (left <= right) {
            if (map.getOrDefault(n[left], '\0') != n[right]) return false;
            left++;
            right--;
        }
        return true;
    }
}
```

```java
class Solution {
    public boolean isStrobogrammatic(String num) {
        String s = "00 11 88 69 96"; // or "00 11 88 696";
        for (int i = 0, j = num.length() - 1; i <= j; i++, j--) {
            String pair = "" + num.charAt(i) + num.charAt(j);
            if (!s.contains(pair)) return false;
        }
        return true;
    }
}
```

### Additional {#additional}



