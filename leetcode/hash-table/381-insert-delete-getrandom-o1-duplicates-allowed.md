### Question {#question}

[https://leetcode.com/problems/insert-delete-getrandom-o1-duplicates-allowed/description/](https://leetcode.com/problems/insert-delete-getrandom-o1-duplicates-allowed/description/)

Design a data structure that supports all following operations inaverage **O\(1\) **time.

**Note: Duplicate elements are allowed.**

1. insert\(val\): Inserts an item val to the collection.
2. remove\(val\): Removes an item val from the collection if present.
3. getRandom: Returns a random element from current collection of elements. The probability of each element being returned is linearly related to the number of same value the collection contains.

**Example:**

```
// Init an empty collection.
RandomizedCollection collection = new RandomizedCollection();

// Inserts 1 to the collection. Returns true as the collection did not contain 1.
collection.insert(1);

// Inserts another 1 to the collection. Returns false as the collection contained 1. Collection now contains [1,1].
collection.insert(1);

// Inserts 2 to the collection, returns true. Collection now contains [1,1,2].
collection.insert(2);

// getRandom should return 1 with the probability 2/3, and returns 2 with the probability 1/3.
collection.getRandom();

// Removes 1 from the collection, returns true. Collection now contains [1,2].
collection.remove(1);

// getRandom should return 1 and 2 both equally likely.
collection.getRandom();
```

### Thought Process {#thought-process}

1. Hash Table and List
   1. Similar to [380-Insert Delete GetRandom O\(1\)](/leetcode/hash-table/380-insert-delete-getrandom-o1.md), we need a hash map to store the mapping between number and its index, but since duplicates are allowed, we need to use a set or a list to store all its indices
   2. We also need list to store number just like last one
   3. To make the adding and removing index for val to achieve O\(1\) time, we use LinkedHashSet
   4. Time complexity O\(1\) insert, O\(1\) remove, and O\(1\) random
   5. Space complexity O\(n\)

### Solution

```java
class RandomizedCollection {
    private Map<Integer, Set<Integer>> indices;
    private List<Integer> numbers;
    private Random random;

    /** Initialize your data structure here. */
    public RandomizedCollection() {
        indices = new HashMap<>();
        numbers = new ArrayList<>();
        random = new Random();
    }
    
    /** Inserts a value to the collection. Returns true if the collection did not already contain the specified element. */
    public boolean insert(int val) {
        boolean contain = indices.containsKey(val);
        if (!contain) indices.put(val, new LinkedHashSet<>());
        indices.get(val).add(numbers.size());
        numbers.add(val);
        return !contain;
    }
    
    /** Removes a value from the collection. Returns true if the collection contained the specified element. */
    public boolean remove(int val) {
        if (!indices.containsKey(val)) return false;
        // remove index from val's index list
        int id = indices.get(val).iterator().next();
        indices.get(val).remove(id);
        if (indices.get(val).isEmpty()) indices.remove(val);
        // removing the number in numbers
        int lastId = numbers.size() - 1;
        if (id < lastId) {
            numbers.set(id, numbers.get(lastId));
            indices.get(numbers.get(lastId)).remove(lastId);
            indices.get(numbers.get(lastId)).add(id);
        }
        numbers.remove(lastId);
        return true;
    }
    
    /** Get a random element from the collection. */
    public int getRandom() {
        return numbers.get(random.nextInt(numbers.size()));
    }
}

/**
 * Your RandomizedCollection object will be instantiated and called as such:
 * RandomizedCollection obj = new RandomizedCollection();
 * boolean param_1 = obj.insert(val);
 * boolean param_2 = obj.remove(val);
 * int param_3 = obj.getRandom();
 */
```

### Additional {#additional}



