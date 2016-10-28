## Group Anagram

Given an array of strings, group anagrams together.

For example, given: `["eat", "tea", "tan", "ate", "nat", "bat"],`
Return:
```
[
  ["ate", "eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

Note: All inputs will be in lower-case.

### Solution

```python
from collections import defaultdict

class Solution(object):
    def groupAnagrams(self, strs):
        """
        :type strs: List[str]
        :rtype: List[List[str]]
        """
        mapper, result = defaultdict(list), []
        for s in strs:
            s_str = "".join(sorted(s))
            mapper[s_str].append(s)
        for a in mapper.values():
            a.sort()
            result.append(a)
        return result


```
