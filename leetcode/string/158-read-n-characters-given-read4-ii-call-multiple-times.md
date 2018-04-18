### Question {#question}

[https://leetcode.com/problems/read-n-characters-given-read4-ii-call-multiple-times/description/](https://leetcode.com/problems/read-n-characters-given-read4-ii-call-multiple-times/description/)

The API: int read4\(char \*buf\) reads 4 characters at a time from a file.

The return value is the actual number of characters read. For example, it returns 3 if there is only 3 characters left in the file.

By using the read4 API, implement the function int read\(char \*buf, int n\) that reads n characters from the file.

**Note:  
**

The read function may be called multiple times.

**Example:**

```

```

### Thought Process {#thought-process}

1. Pick Up where We Left
   1. Because we need to run it multiple time, we need to concern about what we have left when we run it last time
   2. We save previous read character into an array along with the start and end pointer
   3. When we read for current operation, we start from start pointers first until we reach the nth character or run out of character
   4. Then we try again with read4 function as before and save the start and end pointer accordingly for next time
   5. Time complexity O\(n\)
   6. Space complexity O\(1\)

### Solution

```java
/* The read4 API is defined in the parent class Reader4.
      int read4(char[] buf); */

public class Solution extends Reader4 {
    /**
     * @param buf Destination buffer
     * @param n   Maximum number of characters to read
     * @return    The number of characters read
     */
    char[] prev = new char[4];
    int start = 0, end = 0;
    public int read(char[] buf, int n) {
        // start saving the leftover character
        int total = 0, j = Math.min(end, n - total + start);
        while (start < j) buf[total++] = prev[start++];
        while (total < n) {
            start = 0;
            end = read4(prev);
            j = Math.min(end, n - total);
            while (start < j) buf[total++] = prev[start++];
            if (end < 4) break;
        }
        return total;
    }
}
```

### Additional {#additional}



