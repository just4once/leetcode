# 090-subsets-ii

## Question {#question}

[https://leetcode.com/problems/subsets-ii/description/](https://leetcode.com/problems/subsets-ii/description/)

Given a collection of integers that might contain duplicates, **nums**, return all possible subsets \(the power set\).

**Note:**The solution set must not contain duplicate subsets.

**Example:**

```text
If nums = [1,2,2], a solution is:
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```

## Thought Process {#thought-process}

1. Similar to [078-Subsets](078-subsets.md), we need to generate the power sets
2. To remove the duplicate set, we have sort the input and make sure that that current element is not the same as previous element
3. Time complexity O\(2^n\)
4. Space complexity O\(n\)

## Solution

```java
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<List<Integer>> list = new ArrayList<>();
        Arrays.sort(nums);
        backtrack(list, new ArrayList<>(), nums, 0);
        return list;
    }

    public void backtrack(List<List<Integer>> list, List<Integer> path, int[] nums, int start){
        list.add(new ArrayList<>(path));
        for(int i = start; i < nums.length; i++){
            if(i > start && nums[i] == nums[i-1]) continue;
            path.add(nums[i]);
            backtrack(list, path, nums, i + 1);
            path.remove(path.size() - 1);
        }
    }
}
```

## Additional {#additional}

