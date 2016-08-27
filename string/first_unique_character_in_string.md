## First Unique Character in String

Given a string, find the first non-repeating character in it and return it's index. If it doesn't exist, return -1.

Examples:
```
s = "leetcode"
return 0.

s = "loveleetcode",
return 2.
```
Note: You may assume the string contain only lowercase letters.

### Solution

```python
class Solution(object):
    def firstUniqChar(self, s):
        """
        :type s: str
        :rtype: int
        """
        map = {}
        for char in s:
            if char in map.keys():
                map[char] += 1
            else:
                map[char] = 1
        for idx, char in enumerate(s):
            if map[char] == 1:
                return idx
        return -1
```
