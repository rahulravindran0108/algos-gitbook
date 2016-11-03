## Word Pattern

Given a pattern and a string str, find if str follows the same pattern.

Here follow means a full match, such that there is a bijection between a letter in pattern and a non-empty word in str.

Examples:
```
pattern = "abba", str = "dog cat cat dog" should return true.
pattern = "abba", str = "dog cat cat fish" should return false.
pattern = "aaaa", str = "dog cat cat dog" should return false.
pattern = "abba", str = "dog dog dog dog" should return false.
```

Notes:
You may assume pattern contains only lowercase letters, and str contains lowercase letters separated by a single space.

### Solution

```python
class Solution(object):
    def wordPattern(self, pattern, str):
        """
        :type pattern: str
        :type str: str
        :rtype: bool
        """
        lst = str.strip().split(" ")
        if len(pattern) != len(lst):
            return False
        s = set(zip(pattern, lst))

        return len(s) == len(set(pattern)) == len(set(lst))
```
