### Question {#question}

[https://leetcode.com/problems/power-of-three/description/](https://leetcode.com/problems/power-of-three/description/)

Given an integer, write a function to determine if it is a power of three.

**Example:**

```

```

### Thought Process {#thought-process}

1. While Loop
   1. Time complexity O\(log n\)
   2. Space complexity O\(1\)
2. Recursion
   1. Time complexity O\(log n\)
   2. Space complexity O\(log n\)
3. Base Conversion
   1. Leveraging the built-in function in converting number to base form, the base 2 for number that is power of 2 will look like 10\*
   2. Likewise for 3, if we convert the number on the basis of 3, we can match the resulted string with regex
   3. Time complexity O\(log n\)
   4. Space complexity O\(log n\)
4. Math
   1. Since all the integer is range from -2^31 to 2^31 - 1, we can find the maximum power of 3 by find the power first and round down and take the p
   2. int pow = \(int\) \(Math.log\(Integer.MAX\_VALUE\) / Math.log\(3\)\)
   3. int max3power = Math.pow\(3, pow\) = 1162261467
   4. And 3, 9, 27..., all the power of 3 are the only divisors for this number
   5. Time complexity O\(1\)
   6. Space complexity O\(1\)

### Solution

```java
class Solution {
    public boolean isPowerOfThree(int n) {
        if (n < 1) return false;
        while (n % 3 == 0) n /= 3;
        return n == 1;
    }
}
```

```java
class Solution {
    public boolean isPowerOfThree(int n) {
        if (n <= 0) return false;
        if (n == 1) return true;
        return (n % 3 == 0) && isPowerOfThree(n/3);
    }
}
```

```java
class Solution {
    public boolean isPowerOfThree(int n) {
        return Integer.toString(n, 3).matches("^10*$");
    }
}
```

```java
class Solution {
    public boolean isPowerOfThree(int n) {
        int pow = (int) (Math.log(Integer.MAX_VALUE) / Math.log(3));
        return n > 0 && (int) Math.pow(3, pow) % n == 0;
        // return n > 0 && 1162261467 % 3 == 0;
    }
}
```

### Additional {#additional}



