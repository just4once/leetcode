### Question {#question}

Given a blacklist B containing unique integers from \[0, N\), write a function to return a uniform random integer from \[0, N\) which is NOT in B.

Optimize it such that it minimizes the call to system’s Math.random\(\).

**Note:**

1. 1 &lt;= N &lt;= 1000000000
2. 0 &lt;= B.length &lt; min\(100000, N\)
3. \[0, N\) does NOT include N. See interval notation.

**Example 1:**

```
Input: 
["Solution","pick","pick","pick"]
[[1,[]],[],[],[]]
Output: [null,0,0,0]
```

**Example 2:**

```
Input: 
["Solution","pick","pick","pick"]
[[2,[]],[],[],[]]
Output: [null,1,1,1]
```

**Example 3:**

```
Input: 
["Solution","pick","pick","pick"]
[[3,[1]],[],[],[]]
Output: [null,0,0,2]
```

**Example 4:**

```
Input: 
["Solution","pick","pick","pick"]
[[4,[2]],[],[],[]]
Output: [null,1,3,1]
```

**Explanation of Input Syntax:**

The input is two lists: the subroutines called and their arguments. Solution's constructor has two arguments, N and the blacklist B. pick has no arguments. Arguments are always wrapped with a list, even if there aren't any.

### Thought Process {#thought-process}

1. Set \(TLE\)
   1. Use set to save the blacklist and ignore the generated number r if it is inside the set
   2. Time complexity O\(B + x\), where x is times of getting blacklisted item, and the probability = B/N. The x gets worse as B gets close to N
   3. Space complexity O\(B\)
2. Set and List\(TLE\)
   1. Add all the number to the set and then remove the number form blacklist
   2. Time complexity O\(N\)
   3. Space complexity O\(N - B\)
3. asd

### Solution

```java

```

### Additional {#additional}



