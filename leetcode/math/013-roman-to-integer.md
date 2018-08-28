# 013-roman-to-integer

## Question {#question}

[https://leetcode.com/problems/roman-to-integer/description/](https://leetcode.com/problems/roman-to-integer/description/)

Given a roman numeral, convert it to an integer.

Input is guaranteed to be within the range from 1 to 3999.

**Example:**

```text

```

## Thought Process {#thought-process}

1. Map
   1. Putting the character and its value in the map
   2. Compare current value with previous value, if the previous value is smaller that mean we need to decrement the amount by twice, since we "mistakenly" added
   3. Time complexity O\(n\)
   4. Space complexity O\(1\)

## Solution

```java
class Solution {
    public int romanToInt(String s) {
    if (s == null || s.length() == 0) return 0;
    Map<Character, Integer> romanValue = new HashMap<Character, Integer>();
    romanValue.put('I', 1);
    romanValue.put('V', 5);
    romanValue.put('X', 10);
    romanValue.put('L', 50);
    romanValue.put('C', 100);
    romanValue.put('D', 500);
    romanValue.put('M', 1000);

    int total = 0, prevValue = 0;
    for(int i = 0; i < s.length(); ++i) {
           int value = romanValue.get(s.charAt(i));
           if(prevValue < value) total += value - 2 * prevValue;
           else total += value;
           prevValue = value;
        }
    return total;
    }
}
```

```java
class Solution {
    public int romanToInt(String s) {
        if (s == null || s.length() == 0) return 0;
        int total = 0;
        for (int i = s.length() - 1; i >= 0; i--) {
            switch (s.charAt(i)) {
                case 'I' :
                    total += total >= 5 ? -1 : 1;
                    break;
                case 'V' :
                    total += 5;
                    break;
                case 'X':
                    total += total >= 50 ? -10 : 10;
                    break;
                case 'L':
                    total += 50;
                    break;
                case 'C':
                    total += total >= 500 ? -100: 100;
                    break;
                case 'D':
                    total += 500;
                    break;
                case 'M':
                    total += 1000;
                    break;
                default:
                    throw new IllegalArgumentException();
            }
        }
        return total;
    }
}
```

## Additional {#additional}

