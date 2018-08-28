# 038-count-and-say

## Question {#question}

[https://leetcode.com/problems/count-and-say/description/](https://leetcode.com/problems/count-and-say/description/)

The count-and-say sequence is the sequence of integers with the first five terms as following:

```text
1.     1
2.     11
3.     21
4.     1211
5.     111221
```

1 is read off as "one 1" or 11.

11 is read off as "two 1s" or 21.

21 is read off as "one 2, then one 1" or 1211.

**Example:**

## Thought Process {#thought-process}

1. Recursion
   1. Get the previous string and then start count and append
   2. Time complexity ??????
   3. Space complexity O\(n\) due to recursion stack and O\(n\) ??? for storage
2. Iterative
   1. We can also write iterative approach

## Solution

```java
class Solution {
    public String countAndSay(int n) {
        if(n <= 1) return "1";
        String prev = countAndSay(n -1);
        StringBuilder sb = new StringBuilder();
        char[] chars = prev.toCharArray();
        char prevC = chars[0];
        int count = 1;
        for(int i = 1; i < chars.length; i++){
            if (chars[i] == prevC){
                count++;
            } else{
                sb.append(count).append(prevC);
                prevC = chars[i];
                count = 1;
            }
        }
        sb.append(count).append(prevC);
        return sb.toString();
    }
}
```

## Additional {#additional}

