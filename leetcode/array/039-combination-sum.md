# 039-combination-sum

## Question {#question}

[https://leetcode.com/problems/combination-sum/description/](https://leetcode.com/problems/combination-sum/description/)

Given a **set** of candidate numbers \(**C**\)**\(without duplicates\)**and a target number \(**T**\), find all unique combinations in **C** where the candidate numbers sums to**T**.

The **same** repeated number may be chosen from **C** unlimited number of times.

**Note:**

* All numbers \(including target\) will be positive integers.
* The solution set must not contain duplicate combinations.

**Example:**

```text
Given candidate set [2, 3, 6, 7] and target 7, 
A solution set is: 
[
  [7],
  [2, 2, 3]
]
```

## Thought Process {#thought-process}

1. This is classic question asking for use of backtrack
2. We loop through every element, if adding this element will not exceed the target
3. If the target is equal to 0, we have find our solution along this path and we add this path to out solution
4. Time complexity O\(n^2\)
5. Space complexity O\(log n\)

## Solution

```java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> res = new ArrayList<>();
        Arrays.sort(candidates);
        backtrack(res, new ArrayList<>(), candidates, target, 0);
        return res;
    }

    public void backtrack(List<List<Integer>> res, List<Integer> sol, int[] candidates, int target, int start){
        if (target < 0) return;
        else if (target == 0) res.add(new ArrayList<>(sol));
        else {
            for (int i = start; i < candidates.length; i++){
                sol.add(candidates[i]);
                backtrack(res, sol, candidates, target - candidates[i], i);
                sol.remove(sol.size() - 1);
            }
        }
    }
}
```

## Additional {#additional}

