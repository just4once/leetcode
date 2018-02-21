### Question {#question}

[https://leetcode.com/problems/two-sum-iii-data-structure-design/description/](https://leetcode.com/problems/two-sum-iii-data-structure-design/description/)

Design and implement a TwoSum class. It should support the following operations:`add`and`find`.

`add`- Add the number to an internal data structure.  
`find`- Find if there exists any pair of numbers which sum is equal to the value.

**Example:**

```
add(1); add(3); add(5);
find(4) -> true
find(7) -> false
```

### Thought Process {#thought-process}

1. Brute Force - Two Sets \(TLE\)
   1. Use one set to store the numbers, and one set to store the sum
   2. Add will take O\(n\), wrost O\(n^2\)
   3. Find takes O\(1\)
2. ad

### Solution

```java
class TwoSum {
    Set<Integer> num, sum;

    /** Initialize your data structure here. */
    public TwoSum() {
        num = new HashSet<>();
        sum = new HashSet<>();
    }
    
    /** Add the number to an internal data structure.. */
    public void add(int number) {
    	if(num.contains(number)){
    	    sum.add(number * 2);
    	} else{
    	    Iterator<Integer> iter = num.iterator();
    	    while(iter.hasNext()){
    	        sum.add(iter.next() + number);
    	    }
    	    num.add(number);
    	}
    }
    
    /** Find if there exists any pair of numbers which sum is equal to the value. */
    public boolean find(int value) {
        return sum.contains(value);
    }
}

/**
 * Your TwoSum object will be instantiated and called as such:
 * TwoSum obj = new TwoSum();
 * obj.add(number);
 * boolean param_2 = obj.find(value);
 */
```

```java
class TwoSum {
    Map<Integer, Integer> num;

    /** Initialize your data structure here. */
    public TwoSum() {
        num = new HashMap<>();
    }
    
    /** Add the number to an internal data structure.. */
    public void add(int number) {
    	num.put(number, num.getOrDefault(number, 0) + 1);
    }
    
    /** Find if there exists any pair of numbers which sum is equal to the value. */
    public boolean find(int value) {
        Iterator<Integer> iter = num.keySet().iterator();
        while (iter.hasNext()) {
            int num1 = iter.next();
            int num2 = value - num1;
            if (num.containsKey(num2)) {
                if (num1 != num2 || num.get(num2) > 1) return true;
            }
        }
        return false;
    }
}

/**
 * Your TwoSum object will be instantiated and called as such:
 * TwoSum obj = new TwoSum();
 * obj.add(number);
 * boolean param_2 = obj.find(value);
 */
```

### Additional {#additional}



