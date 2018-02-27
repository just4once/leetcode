### Question {#question}

Given a list of unique words, find all pairs of distinct indices \(i, j\) in the given list, so that the concatenation of the two words, i.e. words\[i\] + words\[j\] is a palindrome.

**Example:**

```
Given words = ["bat", "tab", "cat"]
Return [[0, 1], [1, 0]]
The palindromes are ["battab", "tabbat"]

Given words = ["abcd", "dcba", "lls", "s", "sssll"]
Return [[0, 1], [1, 0], [3, 2], [2, 4]]
The palindromes are ["dcbaabcd", "abcddcba", "slls", "llssssll"]
```

### Thought Process {#thought-process}

1. Brute Force
   1. Simply compare two strings can form a palindrome
   2. Time complexity O\(n^2w\), where n is length of list and w is the average length of word
   3. Space complexity O\(1\)
2. Hash Table
   1. Use hashmap to store the string and its index in the map
   2. We need to split the word into two parts at each index and check if there is reversed counter part
      1. if p1 is palindrome, we check if there exists reverse of p2 that we can append in the front
      2. or p2 is palindrome, we check if there exists reverse of p1 that we can append in the end
   3. Corner case is when there is empty string, we need to add all the strings that are palindrome
   4. Time complexity O\(nw^2\)
   5. Space complexity O\(n\)
3. Trie
   1. We can create trie using the reverse of all words
   2. As we going through each word, we need a indicator for identifying if the node is a word
   3. The use of int is especially helpful because not only it can identify a node is a word but also avoid adding same word in the solution set when the word is palindrome
   4. We can also save time by saving the index for current node if the rest of substring is palindrome, when we compare each character to the trie \(reverse order\), which means we can add this word to the front
   5. Time complexity O\(nw^2\)
   6. Space complexity O\(n\)

### Solution

```java
class Solution {
    public List<List<Integer>> palindromePairs(String[] words) {
        List<List<Integer>> res = new ArrayList<>();
        if (words == null || words.length < 2) return res;
        Map<String, Integer> map = new HashMap<>();
        for (int i = 0; i < words.length; i++) {
            map.put(words[i], i);
        }
        for (int i = 0; i < words.length; i++) {
            for (int j = 0; j < words[i].length(); j++) {
                String p1 = words[i].substring(0, j);
                String p2 = words[i].substring(j);
                // if the first part is palindrome, we try to find the reverse of p2
                // to prepend in the front to make palindrome
                if (isPalindrome(p1)) checkReverse(p2, i, map, res, true);
                if (isPalindrome(p2)) checkReverse(p1, i, map, res, false);
            }
        }
        return res;
    }

    private void checkReverse(String s, int i, Map<String, Integer> map, List<List<Integer>> res, boolean addToFront) {
        String sr = reverse(s);
        int id = map.getOrDefault(sr, i);
        if (id != i) {
            if (addToFront) res.add(Arrays.asList(id, i));
            else res.add(Arrays.asList(i, id));
            // this happens when the p2 is the full length, and p1 is empty
            // we can also add the empty string in the front
            if (sr.length() == 0) res.add(Arrays.asList(id, i));
        }
    }

    private String reverse(String s) {
        char[] chars = s.toCharArray();
        int i = 0, j = chars.length - 1;
        while (i < j) {
            char tmp = chars[i];
            chars[i] = chars[j];
            chars[j] = tmp;
            i++;
            j--;
        }
        return String.valueOf(chars);
    }

    private boolean isPalindrome(String s) {
        char[] chars = s.toCharArray();
        int i = 0, j = chars.length - 1;
        while (i < j) {
            if (chars[i] != chars[j]) return false;
            i++;
            j--;
        }
        return true;
    }
}
```

```java
class Solution {
    private static class TrieNode {
        private int index = -1;
        private TrieNode[] next = new TrieNode[26];
        private List<Integer> indices = new ArrayList<>();
    }
    
    public List<List<Integer>> palindromePairs(String[] words) {
        List<List<Integer>> res = new ArrayList<>();
        if (words == null || words.length < 2) return res;
        TrieNode root = new TrieNode();
        for (int i = 0; i < words.length; i++) {
            buildTrie(root, words[i], i);
        }
        for (int i = 0; i < words.length; i++) {
            search(root, words[i], i, res);
        }
        return res;
    }
    
    private void buildTrie(TrieNode root, String word, int i) {
        // creating trie from reversed word
        for (int j = word.length() - 1; j >= 0; j--) {
            int id = word.charAt(j) - 'a';
            if (root.next[id] == null) root.next[id] = new TrieNode();
            if (isPalindrome(word, 0, j)) root.indices.add(i);
            root = root.next[id];
        }
        root.index = i;
        root.indices.add(i);
    }
    
    private void search(TrieNode root, String word, int i, List<List<Integer>> res) {
        for (int j = 0; j < word.length(); j++) {
            if (root.index >= 0 && root.index != i && isPalindrome(word, j, word.length() - 1)) {
                res.add(Arrays.asList(i, root.index));
            }
            root = root.next[word.charAt(j) - 'a'];
            if (root == null) return;
        }
        for (int id : root.indices) {
            if (id == i) continue;
            res.add(Arrays.asList(i, id));
        }
    }
    
    private boolean isPalindrome(String s, int i, int j) {
        while (i < j) {
            if (s.charAt(i++) != s.charAt(j--)) return false;
        }
        return true;
    }
}
```

### Additional {#additional}



