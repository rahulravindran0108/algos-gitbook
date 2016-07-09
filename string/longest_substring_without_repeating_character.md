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