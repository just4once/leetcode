## First Chapter

GitBook allows you to organize your book into chapters, each chapter is stored in a separate file like this one.

```
    public int[] twoSum(int[] nums, int target) {
        if (nums == null) return null;
        int[] result = new int[2];
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int diff = target - nums[i];
            if (map.containsKey(diff)) {
                result[0] = map.get(diff);
                result[1] = i;
                return result;
            }
            map.put(nums[i], i);
        }
        return result;
    }
```



