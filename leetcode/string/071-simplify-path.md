### Question {#question}

[https://leetcode.com/problems/simplify-path/description/](https://leetcode.com/problems/simplify-path/description/)

Given an absolute path for a file \(Unix-style\), simplify it.

**Example:**

```
path = "/home/", => "/home"
path = "/a/./b/../../c/", => "/c"
```

### Thought Process {#thought-process}

1. Deque
   1. Use deque to store the directories
   2. When we encounter "." or "" we continue to next
   3. When we encounter "..", we should pop the last inserted element, just like traveling up the folder
   4. Otherwise, we should save this directory into our queue
   5. Time complexity O\(d\), where d is number of directories
   6. Space complexity O\(n\), where n is the length of path

### Solution

```java
class Solution {
    
    public String simplifyPath(String path) {
        Deque<String> queue = new LinkedList<>();
        for (String dir : path.split("/")) {
		if (dir.equals(".") || dir.equals("")) continue;
		else if (dir.equals("..")) queue.pollLast();
		else queue.add(dir);
	}
	StringBuilder sb = new StringBuilder();
	for (String dir : queue) {
		sb.append("/").append(dir);
	}
	return queue.isEmpty() ? "/" : sb.toString();
    }
}
```

### Additional {#additional}



