### Question {#question}

[https://leetcode.com/problems/restore-ip-addresses/description/](https://leetcode.com/problems/restore-ip-addresses/description/)

Given a string containing only digits, restore it by returning all possible valid IP address combinations.

**Example:**

```
Given "25525511135",

return ["255.255.11.135", "255.255.111.35"]. (Order does not matter)
```

### Thought Process {#thought-process}

1. Backtrack DFS
   1. Using backtrack to track the progress of parsing the string
   2. We have one variable to track the which group we are up to, and another to track the character
   3. Using substring function to break number at different position from 1 to 3, we can check the validity of number
   4. Time complexity O\(3^4\)
   5. Space complexity O\(n\) for path variable
2. Backtrack
   1. Using one char array to store the character and '.' we can speed up the process a bit by avoiding substring
   2. Time complexity O\(3^4\)
   3. Space complexity O\(n\)

### Solution

```java
class Solution {
    public List<String> restoreIpAddresses(String s) {
        List<String> list = new ArrayList<>();
        if(s.length() >= 4 && s.length() <= 12){
            backtrack(list, new String[4], s, 0, 0);
        }
        return list;
    }

    public void backtrack(List<String> list, String[] path, String s, int start, int group){
        if (group == 4) {
            if (start == s.length()) list.add(String.join(".", path));
            return;
        } else {
            for (int i = 1; i <= 3; i++) {
                if (start + i > s.length()) return;
                String section = s.substring(start, start + i);
                if (isValidSection(section)) {
                    path[group] = section;
                    backtrack(list, path, s, start + i, group + 1);
                    path[group] = null;
                }
            }
        }
    }

    private boolean isValidSection(String s){
        if(s.length() < 1 || s.length() > 3 || (s.length() > 1 && s.charAt(0) == '0')) return false;
        return Integer.parseInt(s) < 256;
    }
}
```

```java
class Solution {
    public List<String> restoreIpAddresses(String s) {
        List<String> list = new ArrayList<>();
        if(s.length() >= 4 && s.length() <= 12){
            backtrack(list, new char[s.length() + 3], s.toCharArray(), 0, 0);
        }
        return list;
    }
    
    public void backtrack(List<String> list, char[] path, char[] s, int start, int group){
        if (group == 4) {
            if (start == s.length) list.add(String.valueOf(path));
            return;
        } else {
            int num = 0;
			for (int i = start; i < s.length && i < start + 3; i++) {
                if (s[start] == '0' && i != start) break;
                num = num * 10 + s[i] - '0';
                if (num > 255) break;
                path[group + i] = s[i];
                if (group != 3) path[group + i + 1] = '.';
                backtrack(list, path, s, i + 1, group + 1);
            }
		}
    }
}
```

### Additional {#additional}



