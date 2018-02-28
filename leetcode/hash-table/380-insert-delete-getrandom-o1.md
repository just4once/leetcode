### Question {#question}

[https://leetcode.com/problems/insert-delete-getrandom-o1/description/](https://leetcode.com/problems/insert-delete-getrandom-o1/description/)

Design a data structure that supports all following operations inaverage **O\(1\) **time.

1. insert\(val\): Inserts an item val to the set if not already present.
2. remove\(val\): Removes an item val from the set if present.
3. getRandom: Returns a random element from current set of elements. Each element must have the same probability of being returned.

**Example:**

```
// Init an empty set.
RandomizedSet randomSet = new RandomizedSet();

// Inserts 1 to the set. Returns true as 1 was inserted successfully.
randomSet.insert(1);

// Returns false as 2 does not exist in the set.
randomSet.remove(2);

// Inserts 2 to the set, returns true. Set now contains [1,2].
randomSet.insert(2);

// getRandom should return either 1 or 2 randomly.
randomSet.getRandom();

// Removes 1 from the set, returns true. Set now contains [2].
randomSet.remove(1);

// 2 was already in the set, so return false.
randomSet.insert(2);

// Since 2 is the only number in the set, getRandom always return 2.
randomSet.getRandom();
```

### Thought Process {#thought-process}

1. Hash Map and List
   1. Use hash table to record the number and its index as we grow our list
   2. When we remove, we can move the last item into the removing position and update the map, and then delete the entry in the list and map
   3. Time complexity O\(1\)
   4. Space complexity O\(n\)

### Solution

```java
class RandomizedSet {
    private Map<Integer, Integer> map;
    private List<Integer> list;
    private Random random;
    /** Initialize your data structure here. */
    public RandomizedSet() {
        list = new ArrayList<>();
        map = new HashMap<>();
        random = new Random();
    }
    
    /** Inserts a value to the set. Returns true if the set did not already contain the specified element. */
    public boolean insert(int val) {
        if (map.containsKey(val)) return false;
        map.put(val, list.size());
        return list.add(val);
    }
    
    /** Removes a value from the set. Returns true if the set contained the specified element. */
    public boolean remove(int val) {
        if (!map.containsKey(val)) return false;
        int index = map.get(val);
        int lastIndex = list.size() - 1;
        if (index < lastIndex) {
            int tmp = list.get(lastIndex);
            list.set(index, tmp);
            map.put(tmp, index);
        }
        map.remove(val);
        list.remove(lastIndex);
        return true;
    }
    
    /** Get a random element from the set. */
    public int getRandom() {
        int r = random.nextInt(list.size());
        return list.get(r);
    }
}

/**
 * Your RandomizedSet object will be instantiated and called as such:
 * RandomizedSet obj = new RandomizedSet();
 * boolean param_1 = obj.insert(val);
 * boolean param_2 = obj.remove(val);
 * int param_3 = obj.getRandom();
 */
```

### Additional {#additional}



