## Minimum Window Substring

Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).

```
For example,
S = "ADOBECODEBANC"
T = "ABC"
Minimum window is "BANC".
```

### Solution

```java
public class Solution {
    public String minWindow(String s, String t) {
        int [] hash = new int[256];

        for(char c : t.toCharArray())
            hash[c]++;

        int counter = t.length(), begin = 0, end = 0, head = 0;
        int answer = Integer.MAX_VALUE;

        while(end < s.length()) {
            if(hash[s.charAt(end)] > 0)
                counter--;
            hash[s.charAt(end)]--;
            end++;


            while(counter == 0) {
                if(end-begin<answer) {
                    answer = end - begin;
                    head = begin;
                }

                hash[s.charAt(begin)]++;
			    if (hash[s.charAt(begin)] > 0)
				    counter++;
			    begin++;
            }
        }
        return answer == Integer.MAX_VALUE ? "" : s.substring(head, head + answer);
    }
}
```
