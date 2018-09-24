# 215-kth-largest-element-in-an-array

## Question {#question}

[https://leetcode.com/problems/kth-largest-element-in-an-array/description/](https://leetcode.com/problems/kth-largest-element-in-an-array/description/)

Find the **k** th largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

**Example 1:**

```text
Input: [3,2,1,5,6,4] and k = 2
Output: 5
```

**Example 2:**

```text
Input: [3,2,3,1,2,4,5,5,6] and k = 4
Output: 4
```

**Note:**   
You may assume k is always valid, 1 ≤ k ≤ array's length.

## Thought Process {#thought-process}

1. MinHeap
   1. Use min heap to store up to K elements
   2. Everytime, when the heap is full, we poll one out
   3. At the end the process the Kth largest element in at the top
   4. Time complexity O\(nlogk\)
   5. Space complexity O\(K\)
2. QuickSelect
   1. Using quick select we can optimize the algorithm's complexity to be O\(n\)
   2. Space complexity O\(1\)

## Solution

```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        for (int num : nums) {
            pq.offer(num);
            if (pq.size() > k) pq.poll();
        }
        return pq.peek();
    }
}
```

```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        int lo = 0, hi = nums.length - 1;
        k = nums.length - k;
        while (lo < hi) {
            int pivotId = quickSelect(nums, lo, hi);
            if (pivotId == k) return nums[k];
            else if (pivotId < k) lo = pivotId + 1;
            else hi = pivotId - 1;
        }
        return nums[lo];
    }
    
    private int quickSelect(int[] nums, int lo, int hi) {
        int pivot = lo;
        while (lo <= hi) {
            while (lo <= hi && nums[lo] <= nums[pivot]) lo++;
            while (lo <= hi && nums[hi] > nums[pivot]) hi--;
            if (lo >= hi) break;
            swap(nums, lo, hi);
        }
        swap(nums, pivot, hi);
        return hi;
    }
    
    private void swap(int[] nums, int i, int j) {
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
}
```

## Additional {#additional}

