### Question {#question}

[https://leetcode.com/problems/bulb-switcher/description/](https://leetcode.com/problems/bulb-switcher/description/)

There are n bulbs that are initially off. You first turn on all the bulbs. Then, you turn off every second bulb. On the third round, you toggle every third bulb \(turning on if it's off or turning off if it's on\). For the ith round, you toggle every i bulb. For the nth round, you only toggle the last bulb. Find how many bulbs are on after n rounds.

**Example:**

```

```

### Thought Process {#thought-process}

1. Perfect Square
   1. Observe that only perfect square will be switched odd number of times, resulting "on" status
   2. Total number of time will be the sqrt of input
   3. Time complexity O\(1\)
   4. Space complexity O\(1\)

### Solution

```java
class Solution {
    public int bulbSwitch(int n) {
        return (int) Math.sqrt(n);
    }
}
```

### Additional {#additional}



