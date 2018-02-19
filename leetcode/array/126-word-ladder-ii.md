### Question {#question}

[https://leetcode.com/problems/word-ladder-ii/description/](https://leetcode.com/problems/word-ladder-ii/description/)

Given two words \(beginWordandendWord\), and a dictionary's word list, find all shortest transformation sequence\(s\) frombeginWordtoendWord, such that:

1. Only one letter can be changed at a time
2. Each transformed word must exist in the word list. Note that beginWord is not a transformed word.

**Example:**

```
Given:
beginWord = "hit"
endWord = "cog"
wordList = ["hot","dot","dog","lot","log","cog"]

Return
  [
    ["hit","hot","dot","dog","cog"],
    ["hit","hot","lot","log","cog"]
  ]
```

**Note:**

* Return an empty list if there is no such transformation sequence.
* All words have the same length.
* All words contain only lowercase alphabetic characters.
* You may assume no duplicates in the word list.
* You may assume beginWord and endWord are non-empty and are not the same.

### Thought Process {#thought-process}

1. Dijkstra's search
   1. We need to track the distance of each node from the source and their parent\(s\)
   2. Unlike regular Dijkstra search where we only care about one parent, we need to save all their parents
   3. The steps involves, initialization, pulling the min vertex, and relaxation
   4. Time complexity O\(nw\)???
   5. Space complexity O\(n\) ???
2. One End Search
   1. We put the begin word in the "begin set"
   2. For every word in the begin set, we generate the permutation
   3. When one the permutation is the final word, the shortest path has been found. However, we still need to search through all the permutation of the word in the beginner set to be complete
   4. Time complexity O\(k^d\), where k is the average permutations for word, and d is the steps to reach to the endWord
   5. Space complexity O\(n\)???
3. Two End Search
   1. The search time will speed up by exponential from O\(k^d\) to O\(k^\(d/2\)\)
   2. One thing, we need to be careful is that when we reverse the begin set and end set, we need to reverse the key we insert into the map for storing the parents
   3. Space complexity O\(n\)????

### Solution

Dijkstra's search

```java
class Solution {
    public List<List<String>> findLadders(String beginWord, String endWord, List<String> wordList) {
        // We can leverage the Dijkstra's search, we poll the node out and relaxed its neighbor.
        // We also need a way to store the parent, or the edge that lead to the node, so we can 
        // reconstruct the path. Unlike regular Dijkstra's search where we only care about one
        // parent, this question wants all the shortest path, therefore we need a Map from string
        // to an array list.
        Set<String> dict = new HashSet<>();
        Map<String, List<String>> parents = new HashMap<>();
        Map<String, Integer> distance = new HashMap<>();
        // Initialization
        for (String word : wordList) {
            dict.add(word);
            distance.put(word, Integer.MAX_VALUE);
        }
        List<List<String>> res = new ArrayList<>();
        if (!dict.contains(endWord)) return res;
        distance.put(beginWord, 0);
        Queue<String> q = new LinkedList<>();
        q.add(beginWord);
        int min = Integer.MAX_VALUE;
        while (!q.isEmpty()) {
            String cur = q.poll();
            int d = distance.get(cur) + 1;
            if (d > min) break;
            for (String nei : getNeighbors(cur, dict)) {
                // relaxation
                if (d > distance.get(nei)) {
                    continue;
                } else if (d < distance.get(nei)) {
                    q.offer(nei);
                    distance.put(nei, d);
                }
                parents.computeIfAbsent(nei, k -> new ArrayList<>()).add(cur);
                if (nei.equals(endWord)) min = d;
            }
        }
        LinkedList<String> path = new LinkedList<>();
        path.add(endWord);
        backtrack(endWord, beginWord, parents, res, path);
        return res;
    }

    private void backtrack(String word, String beginWord, Map<String, List<String>> parents, List<List<String>> res, LinkedList<String> path) {
        if (word.equals(beginWord)) {
            res.add(new LinkedList<>(path));
            return;
        }
        if (!parents.containsKey(word)) return;
        for (String parent : parents.get(word)) {
            path.addFirst(parent);
            backtrack(parent, beginWord, parents, res, path);
            path.removeFirst();
        }
    }

    private Set<String> getNeighbors(String word, Set<String> dict) {
        char[] chars = word.toCharArray();
        Set<String> set = new HashSet<>();
        for (int i = 0; i < chars.length; i++) {
            char c = chars[i];
            for (char a = 'a'; a <= 'z'; a++) {
                if (a == c) continue;
                chars[i] = a;
                String tmp = new String(chars);
                if (dict.contains(tmp)) {
                    set.add(tmp);
                }
            }
            chars[i] = c;
        }
        return set;
    }
}
```

One End

```java
class Solution {
    public List<List<String>> findLadders(String beginWord, String endWord, List<String> wordList) {
        // Single end approach, we stop when we reach the endword.
        // We generate words for each level, and continue the search
        Set<String> dict = new HashSet<>(wordList);
        List<List<String>> res = new ArrayList<>();
        if (!dict.contains(endWord)) return res;
        Map<String, List<String>> map = new HashMap<>();
        Set<String> begin = new HashSet<>(), end = new HashSet<>();
        begin.add(beginWord);
        end.add(endWord);
        dict.remove(beginWord);
        bfs(begin, end, map, dict);
        List<String> path = new ArrayList<>();
        path.add(beginWord);
        dfs(beginWord, endWord, map, path, res);
        return res;
    }

    private void bfs(Set<String> begin, Set<String> end, Map<String, List<String>> map, Set<String> dict) {
        if (begin.isEmpty()) return;
        boolean done = false;
        Set<String> next = new HashSet<>();
        for (String w : begin) {
            for (String nei : getNeighbors(w, dict)) {
                // if the end contains our final word, we are done
                if (end.contains(nei)) done = true;
                // Add the neighbor for next search
                if (!done) next.add(nei);
                map.computeIfAbsent(w, k -> new ArrayList<>()).add(nei);
            }
        }
        if (!done) {
            dict.removeAll(next);
            bfs(next, end, map, dict);
        }
    }

    private void dfs(String cur, String endWord, Map<String, List<String>> map, List<String> path, List<List<String>> res) {
        if (cur.equals(endWord)) {
            res.add(new ArrayList<>(path));
            return;
        }
        if (!map.containsKey(cur)) return;
        for (String nei : map.get(cur)) {
            path.add(nei);
            dfs(nei, endWord, map, path, res);
            path.remove(path.size() - 1);
        }
    }

    private Set<String> getNeighbors(String word, Set<String> dict) {
        char[] chars = word.toCharArray();
        Set<String> set = new HashSet<>();
        for (int i = 0; i < chars.length; i++) {
            char c = chars[i];
            for (char a = 'a'; a <= 'z'; a++) {
                if (a == c) continue;
                chars[i] = a;
                String tmp = new String(chars);
                if (dict.contains(tmp)) {
                    set.add(tmp);
                }
            }
            chars[i] = c;
        }
        return set;
    }
}
```

Two End

```java
class Solution {
    public List<List<String>> findLadders(String beginWord, String endWord, List<String> wordList) {
        // Single end approach, we stop when we reach the endword.
        // We generate words for each level, and continue the search
        Set<String> dict = new HashSet<>(wordList);
        List<List<String>> res = new ArrayList<>();
        if (!dict.contains(endWord)) return res;
        Map<String, List<String>> map = new HashMap<>();
        Set<String> begin = new HashSet<>(), end = new HashSet<>();
        begin.add(beginWord);
        end.add(endWord);
        bfs(begin, end, map, dict, false);
        System.out.println(map);
        List<String> path = new ArrayList<>();
        path.add(beginWord);
        dfs(beginWord, endWord, map, path, res);
        return res;
    }

    private void bfs(Set<String> begin, Set<String> end, Map<String, List<String>> map, Set<String> dict, boolean flip) {
        boolean done = false;
        Set<String> next = new HashSet<>();
        dict.removeAll(begin);
        for (String w : begin) {
            for (String nei : getNeighbors(w)) {
                if (dict.contains(nei)) {
                    String key = flip ? nei : w;
                    String val = flip ? w : nei;
                    // if the end contains our final word, we are done
                    if (end.contains(nei)) done = true;
                    // Add the neighbor for next search
                    else next.add(nei);
                    map.computeIfAbsent(key, k -> new ArrayList<>()).add(val);
                }
            }
        }
        if (!done && !next.isEmpty()) {
            if (next.size() > end.size()) bfs(end, next, map, dict, !flip);
            else bfs(next, end, map, dict, flip);
        }
    }

    private void dfs(String cur, String endWord, Map<String, List<String>> map, List<String> path, List<List<String>> res) {
        if (cur.equals(endWord)) {
            res.add(new ArrayList<>(path));
            return;
        }
        if (!map.containsKey(cur)) return;
        for (String nei : map.get(cur)) {
            path.add(nei);
            dfs(nei, endWord, map, path, res);
            path.remove(path.size() - 1);
        }
    }

    private Set<String> getNeighbors(String word) {
        char[] chars = word.toCharArray();
        Set<String> set = new HashSet<>();
        for (int i = 0; i < chars.length; i++) {
            char c = chars[i];
            for (char a = 'a'; a <= 'z'; a++) {
                if (a == c) continue;
                chars[i] = a;
                String tmp = new String(chars);
                set.add(tmp);
            }
            chars[i] = c;
        }
        return set;
    }
}
```

### Additional {#additional}



