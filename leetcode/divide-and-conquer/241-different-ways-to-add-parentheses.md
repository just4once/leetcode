# 241-different-ways-to-add-parentheses

## Question {#question}

Given a string of numbers and operators, return all possible results from computing all the different possible ways to group numbers and operators. The valid operators are `+`, `-` and `*`.

**Example 1:**

```text
Input: "2-1-1"
Output: [0, 2]
Explanation: 
((2-1)-1) = 0 
(2-(1-1)) = 2
```

**Example 2:**

```text
Input: "2*3-4*5"
Output: [-34, -14, -10, -10, 10]
Explanation: 
(2*(3-(4*5))) = -34 
((2*3)-(4*5)) = -14 
((2*(3-4))*5) = -10 
(2*((3-4)*5)) = -10 
(((2*3)-4)*5) = 10
```

## Thought Process {#thought-process}

1. Divide and Conquer
   1. Divide the input string into two different parts every time we encounter a operator
   2. From the return list, we can add the corresponding value based on operators to our list
   3. Time complexity O\(3^n\)
   4. Space complexity O\(3^n\)
2. 
## Solution

```java

```

## Additional {#additional}

