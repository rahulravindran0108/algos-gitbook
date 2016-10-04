## Longest Common Prefix

Write a function to find the longest common prefix string amongst an array of strings.

### Solution

```python
class Solution(object):
    def longestCommonPrefix(self, strs):
        """
        :type strs: List[str]
        :rtype: str
        """
        if not strs:
            return ""
        base_str = strs[0]

        for i in range(len(base_str)):
            for j in strs:
                if i >= len(j) or base_str[i] != j[i]:
                    return base_str[:i]
        return base_str

```
