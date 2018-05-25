### Question {#question}

[https://leetcode.com/problems/heaters/description/](https://leetcode.com/problems/heaters/description/)

Winter is coming! Your first job during the contest is to design a standard heater with fixed warm radius to warm all the houses.

Now, you are given positions of houses and heaters on a horizontal line, find out minimum radius of heaters so that all houses could be covered by those heaters.

So, your input will be the positions of houses and heaters seperately, and your expected output will be the minimum radius standard of heaters.

**Note:**

1. Numbers of houses and heaters you are given are non-negative and will not exceed 25000.
2. Positions of houses and heaters you are given are non-negative and will not exceed 10^9.
3. As long as a house is in the heaters' warm radius range, it can be warmed.
4. All the heaters follow your radius standard and the warm radius will the same.

**Example 1:**

```
Input: [1,2,3],[2]
Output: 1
Explanation: The only heater was placed in the position 2, and if we use the radius 1 standard, then all the houses can be warmed.
```

**Example 2:**

```
Input: [1,2,3,4],[1,4]
Output: 1
Explanation: The two heater was placed in the position 1 and 4. We need to use radius 1 standard, then all the houses can be warmed.
```

### Thought Process {#thought-process}

1. Sort and Binary Search
   1. Sort Heaters array and perform binary search on the house
   2. If the returned index is greater or equal to zero, ,that means the house is located right on heater, we can ignore it
   3. If the returned index is smaller than 0, we can have find the left and right heater for this house and get the radius \(left will be i -1th and right will be ith position\)
   4. The min of the radii will compare with the res, and the max of them is our temporary res
   5. Time complexity O\(nlogn\)
   6. Space complexity O\(1\)
2. Sort and Two Pointers
   1. If we sort both arrays, we just need to find the first heater that is closest to the house
   2. Then the result is simply the max of distance between the house-heater and the previous res
   3. To find the closest heater, we use while loop until we get the heater that is closer than previous heater
   4. Time complexity O\(nlogn + mlogn\)
   5. Space complexity O\(1\)

### Solution

```java
class Solution {
    public int findRadius(int[] houses, int[] heaters) {
        Arrays.sort(heaters);
        int n = heaters.length;
        int r = 0;
        for (int house : houses) {
            int i = Arrays.binarySearch(heaters, house);
            if (i < 0) {
                i = -(i + 1);
                int leftR = i > 0 ? house - heaters[i - 1] : Integer.MAX_VALUE;
                int rightR = i < n ? heaters[i] - house : Integer.MAX_VALUE;
                r = Math.max(r, Math.min(leftR, rightR));
            }
        }
        return r;
    }
}
```

```java
class Solution {
    public int findRadius(int[] houses, int[] heaters) {
        Arrays.sort(heaters);
        Arrays.sort(houses);
        int n = heaters.length;
        int r = 0, h = 0;
        for (int house : houses) {
            while (h < n - 1 && Math.abs(heaters[h + 1] - house) <= Math.abs(heaters[h] - house)) h++;
            r = Math.max(r, Math.abs(heaters[h] - house));
        }
        return r;
    }
}
```

### Additional {#additional}



