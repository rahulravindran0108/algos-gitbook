## Longest Substring Without Repeating Characters

Given a string, find the length of the longest substring without repeating characters.

Examples:

Given "abcabcbb", the answer is "abc", which the length is 3.

Given "bbbbb", the answer is "b", with the length of 1.

Given "pwwkew", the answer is "wke", with the length of 3. Note that the answer must be a substring, "pwke" is a subsequence and not a substring.

### Solution

```python
class Solution(object):
    def lengthOfLongestSubstring(self, s):
        """
        :type s: str
        :rtype: int
        """
        start, maxlen = 0,0
        dict = {}
        for i in range(len(s)):
            dict[s[i]] = -1

        for i in range(len(s)):
            if dict[s[i]] != -1:
                while start <= dict[s[i]]:
                    dict[start] = -1
                    start+=1
            if i - start + 1 > maxlen: maxlen = i - start + 1
            dict[s[i]] = i
        return maxlen
```

```java
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        Map<Character, Integer> map = new HashMap<>();
        int maxLength = 0;
        int start = 0;

        for(int i = 0;i<s.length();i++) {
            if(map.containsKey(s.charAt(i))) {
                maxLength = Math.max(maxLength, i - start);
                int j = map.get(s.charAt(i));
                while(start <= j) {
                    map.remove(s.charAt(start));
                    start ++;
                }

            }

            map.put(s.charAt(i), i);
        }

        maxLength = Math.max(maxLength, s.length() - start);

        return maxLength;
    }
}
```
