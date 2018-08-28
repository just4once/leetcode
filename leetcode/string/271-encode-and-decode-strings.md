# 271-encode-and-decode-strings

## Question {#question}

[https://leetcode.com/problems/encode-and-decode-strings/description/](https://leetcode.com/problems/encode-and-decode-strings/description/)

Design an algorithm to encode a list of strings to a string. The encoded string is then sent over the network and is decoded back to the original list of strings.

Machine 1 \(sender\) has the function:

```text
string encode(vector<string> strs) {
  // ... your code
  return encoded_string;
}
```

Machine 2 \(receiver\) has the function:

```text
vector<string> decode(string s) {
  //... your code
  return strs;
}
```

So Machine 1 does:

```text
string encoded_string = encode(strs);
```

and Machine 2 does:

```text
vector<string> strs2 = decode(encoded_string);
```

strs2 in Machine 2 should be the same as strs in Machine 1.

Implement the encode and decode methods.

## Thought Process {#thought-process}

1. Delimiter and String Length
   1. Using simple symbol such as '/' or '-' won't work because that could be part of the string as well
   2. Instead, we append the length of string first, along with chosen delimiter, '/'
   3. Then we know exactly how long is the string and where to break
   4. Time complexity O\(n\), where n is number of string
   5. Space complexity O\(nw\), where w is the average length of words
2. asd

## Solution

```java
public class Codec {

    // Encodes a list of strings to a single string.
    public String encode(List<String> strs) {
        StringBuilder sb = new StringBuilder();
        for(String str : strs) {
            sb.append(str.length()).append('/').append(str);
        }
        return sb.toString();
    }

    // Decodes a single string to a list of strings.
    public List<String> decode(String s) {
        int i = 0;
        List<String> res = new ArrayList<>();
        while (i < s.length()) {
            int slash = s.indexOf('/', i);
            int len = Integer.valueOf(s.substring(i, slash));
            int next = slash + len + 1;
            res.add(s.substring(slash + 1, next));
            i = next;
        }
        return res;
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.decode(codec.encode(strs));
```

## Additional {#additional}

