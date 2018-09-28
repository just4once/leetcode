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
2. Divide and Conquer \(Cached\)
   1. Avoid repetitive calculation
   2. Time complexity O\(?\)
   3. Space complexity o\(?\)
3. asd

## Solution

```java
class Solution {
    public List<Integer> diffWaysToCompute(String input) {
        List<Integer> res = new ArrayList<>();
        for (int i = 0; i < input.length(); i++) {
            char c = input.charAt(i);
            if (c == '+' || c == '-' || c == '*') {
                List<Integer> left = diffWaysToCompute(input.substring(0, i));
                List<Integer> right = diffWaysToCompute(input.substring(i + 1, input.length()));
                for (int n1 : left) {
                    for (int n2 : right) {
                        if (c == '+') res.add(n1 + n2);
                        else if (c == '-') res.add(n1 - n2);
                        else res.add(n1 * n2);
                    }
                }
            }
        }
        if (res.size() == 0) res.add(Integer.parseInt(input));
        return res;
    }
}
```

```java
class Solution {
    
    public List<Integer> diffWaysToCompute(String input) {
        // Use cache to avoid repeative calculaiton
        Map<String, List<Integer>> cache = new HashMap<>();
        return search(input, cache);
    }
    
    private List<Integer> search(String input, Map<String, List<Integer>> cache) {
        if (cache.containsKey(input)) return cache.get(input);
        List<Integer> res = new ArrayList<>();
        for (int i = 0; i < input.length(); i++) {
            char c = input.charAt(i);
            if (c == '+' || c == '-' || c == '*') {
                List<Integer> left = diffWaysToCompute(input.substring(0, i));
                List<Integer> right = diffWaysToCompute(input.substring(i + 1, input.length()));
                for (int n1 : left) {
                    for (int n2 : right) {
                        if (c == '+') res.add(n1 + n2);
                        else if (c == '-') res.add(n1 - n2);
                        else res.add(n1 * n2);
                    }
                }
            }
        }
        if (res.size() == 0) res.add(Integer.parseInt(input));
        cache.put(input, res);
        return res;
    }
}
```

## Additional {#additional}

