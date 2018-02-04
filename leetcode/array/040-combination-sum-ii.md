### Question {#question}

[https://leetcode.com/problems/combination-sum-ii/description/](https://leetcode.com/problems/combination-sum-ii/description/)

Given a collection of candidate numbers \(**C**\) and a target number \(**T**\), find all unique combinations in**C**where the candidate numbers sums to**T**.

Each number in**C**may only be used**once**in the combination.

**Note:**  


* All numbers \(including target\) will be positive integers.
* The solution set must not contain duplicate combinations.

**Example:**

```
For example, given candidate set [10, 1, 2, 7, 6, 1, 5] and target 8, 
A solution set is: 
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
```

### Thought Process {#thought-process}

1. To avoid the duplicated solution, we have to sort the input
2. If the number is the same as the last number, we skip them
3. We also have to use backtrack to keep track of the number added
4. We could also break early if the current element will greater than the target since input was sorted at step 1
5. Time complexity O\(n^2\)
6. Space complexity O\(log n\)

### Solution

```java
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> res = new ArrayList<>();
        Arrays.sort(candidates);
        backtrack(res, new ArrayList<>(), candidates, target, 0);
        return res;
    }
    
    public void backtrack(List<List<Integer>> res, List<Integer> sol, int[] candidates, int target, int start){
        if (target == 0) res.add(new ArrayList<>(sol));
        else {
            for(int i = start; i < candidates.length; i++){
                if(i > start && candidates[i] == candidates[i-1]) continue;
                if (candidates[i] > target) break;
                sol.add(candidates[i]);
                backtrack(res, sol, candidates, target - candidates[i], i + 1);
                sol.remove(sol.size() - 1);
            }
        }
    }
}
```

### Additional {#additional}



