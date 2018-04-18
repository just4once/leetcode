### Question {#question}

[https://leetcode.com/problems/read-n-characters-given-read4/description/](https://leetcode.com/problems/read-n-characters-given-read4/description/)

The API: int read4\(char \*buf\) reads 4 characters at a time from a file.

The return value is the actual number of characters read. For example, it returns 3 if there is only 3 characters left in the file.

By using the read4 API, implement the function int read\(char \*buf, int n\) that reads n characters from the file.

**Example:**

```

```

**Note:**

The read function will only be called once for each test case.

### Thought Process

1. Extra Buffer Array and Pointer
   1. Read and store the characters in a temporary buffer
   2. Then append the character until we reach the end of file or the nth character
   3. Time complexity O\(n\)
   4. Space complexity O\(1\)

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
    public int read(char[] buf, int n) {
        char[] tmp = new char[4];
        int total = 0;
        while (total < n) {
            int count = read4(tmp);
            int len = Math.min(count, n - total);
            for (int i = 0; i < len; i++) {
                buf[total++] = tmp[i];
            }
            if (count < 4) break;
        }
        return total;
    }
}Additional
```



