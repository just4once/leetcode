# 264-ugly-number-ii

## Question {#question}

[https://leetcode.com/problems/ugly-number-ii/description/](https://leetcode.com/problems/ugly-number-ii/description/)

Write a program to find the n-th ugly number.

Ugly numbers are positive numbers whose prime factors only include 2, 3, 5. For example, 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 is the sequence of the first 10 ugly numbers.

Note that 1 is typically treated as an ugly number, and n does not exceed 1690.

**Example:**

```text

```

## Thought Process {#thought-process}

1. PriorityQueue
   1. Every number polled out, we multiply by 2, 3, and 5 and add it back to queue
   2. We also make sure we avoid the duplicate by polling the number that is equal to current value
   3. Time complexity O\(n logn\)
   4. Space complexity O\(n\)
2. Three Pointers
   1. We use an array to store the ugly number
   2. We use three pointer to track the last number use for each factor 2, 3, and 5
   3. The next number is the min of three numbers times their corresponding indexed number
   4. Increment index for the factors that matches the current ugly number
   5. Time complexity O\(n\)
   6. Space complexity O\(n\)

## Solution

```java
class Solution {
    public int nthUglyNumber(int n) {
        PriorityQueue<Long> pq = new PriorityQueue<>();
        pq.add(1L);
        long lastUgly = 0L;
        for (int i = 0; i < n; i++) {
            lastUgly = pq.poll();
            while (!pq.isEmpty() && pq.peek() == lastUgly) pq.poll();
            pq.add(lastUgly * 2);
            pq.add(lastUgly * 3);
            pq.add(lastUgly * 5);
        }
        return (int) lastUgly;
    }
}
```

```java
class Solution {
    public int nthUglyNumber(int n) {
        int[] ugly = new int[n];
        ugly[0] = 1;
        int i2 = 0, i3 = 0, i5 = 0;
        // the logic is by maintaining three indices pointing to last unused numbers,
        // we know what is the next ugly must be the min of each of them multiply by
        // their group multiplier, i.e. 2, 3, 5.
        for (int i = 1; i < n; i++) {
            ugly[i] = Math.min(ugly[i2] * 2, Math.min(ugly[i3] * 3, ugly[i5] * 5));
            if (ugly[i] == ugly[i2] * 2) i2++;
            if (ugly[i] == ugly[i3] * 3) i3++;
            if (ugly[i] == ugly[i5] * 5) i5++;
        }
        return ugly[n - 1];
    }
}
```

## Additional {#additional}

