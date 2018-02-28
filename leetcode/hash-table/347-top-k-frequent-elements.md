### Question {#question}

[https://leetcode.com/problems/top-k-frequent-elements/description/](https://leetcode.com/problems/top-k-frequent-elements/description/)

Given a non-empty array of integers, return the **k **most frequent elements.

**Example:**

```
Given [1,1,1,2,2,3] and k = 2, return [1,2].
```

### Thought Process {#thought-process}

1. Max Heap
   1. Count the frequency of each number
   2. Store all the entries in the max heap
   3. Poll the top element into out result list
   4. Time complexity O\(n logn\)
   5. Space complexity O\(n\)
2. Min Heap
   1. Time complexity O\(n log k\)
   2. Space complexity O\(k\)
3. Tree Map
   1. Time complexity O\(n log n\) from treemap
   2. Space complexity O\(log n\)
4. Bucket Sort
   1. Use the frequency as the index for bucket sort, we add the most frequent elements down to less frequent one until we have k elements
   2. Time complexity O\(n\)
   3. Space complexity O\(n\)

### Solution

```java
class Solution {
    public List<Integer> topKFrequent(int[] nums, int k) {
        int n = nums.length;
        List<Integer> res = new ArrayList<>();
        Map<Integer, Integer> map = new HashMap<>();
        for (int num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);
        }
        Queue<Map.Entry<Integer, Integer>> maxHeap = new PriorityQueue<>((a, b) -> b.getValue() - a.getValue());
        maxHeap.addAll(map.entrySet());
        while (res.size() < k) res.add(maxHeap.poll().getKey());
        return res;
    }
}
```

```java
class Solution {
    public List<Integer> topKFrequent(int[] nums, int k) {
        int n = nums.length;
        LinkedList<Integer> res = new LinkedList<>();
        Map<Integer, Integer> map = new HashMap<>();
        for (int num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);
        }
        Queue<Map.Entry<Integer, Integer>> minHeap = new PriorityQueue<>((a, b) -> a.getValue() - b.getValue());
        for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
            minHeap.add(entry);
            if (minHeap.size() > k) minHeap.poll();
        }
        while (!minHeap.isEmpty()) res.addFirst(minHeap.poll().getKey());
        return res;
    }
}
```

```java
class Solution {
    public List<Integer> topKFrequent(int[] nums, int k) {
        int n = nums.length;
        LinkedList<Integer> res = new LinkedList<>();
        Map<Integer, Integer> map = new HashMap<>();
        for (int num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);
        }
        TreeMap<Integer, List<Integer>> tree = new TreeMap<>();
        for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
            tree.putIfAbsent(entry.getValue(), new ArrayList<>());
            tree.get(entry.getValue()).add(entry.getKey());
        }
        while (res.size() < k) {
            res.addAll(tree.pollLastEntry().getValue());
        }
        return res;
    }
}
```

```java
class Solution {
    public List<Integer> topKFrequent(int[] nums, int k) {
        int n = nums.length;
        List<Integer> res = new ArrayList<>();
        Map<Integer, Integer> map = new HashMap<>();
        for (int num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);
        }
        // use the freq as the index, the nums can have at most n frequency
        List<Integer>[] bucket = new ArrayList[n + 1];
        for (int key : map.keySet()) {
            if (bucket[map.get(key)] == null)  bucket[map.get(key)] = new ArrayList<>();
            bucket[map.get(key)].add(key);
        }
        for (int i = n; i >= 0 && res.size() < k; i--) {
            if (bucket[i] != null) {
                res.addAll(bucket[i]);
            }
        }
        return res;
    }
}
```

### Additional {#additional}



