### Question {#question}

[https://leetcode.com/problems/subsets/description/](https://leetcode.com/problems/subsets/description/)

Given a set of **distinct **integers, nums, return all possible subsets \(the power set\).

**Note:**The solution set must not contain duplicate subsets.

**Example:**

```
If nums = [1,2,3], a solution is:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

### Thought Process {#thought-process}

1. For creating power set, there are 2^n possibilities, where n is number of elements, due to each element can be either in or out of particular set
2. To help create the set, we can have an additional array

### Solution

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        backtrack(nums, res, new ArrayList<>(), 0);
        return res;
    }

    public void backtrack(int[] nums, List<List<Integer>> res, List<Integer> path, int start) {
        res.add(new ArrayList<>(path));
        for (int i = start; i < nums.length; i++) {
            path.add(nums[i]);
            backtrack(nums, res, path, i + 1);
            path.remove(path.size() - 1);
        }
    }
}
```

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        if (nums == null || nums.length == 0) return res;
        res.add(new ArrayList<>());
        for (int i = 0; i < nums.length; i++) {
            int size = res.size();
            for (int j = 0; j < size; j++) {
                List<Integer> l = new ArrayList<>(res.get(j));
                l.add(nums[i]);
                res.add(l);
            }
        }
        return res;
    }
}
```

### Additional {#additional}



