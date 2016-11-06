## Roman to Integer

### Solution

```python
class Solution(object):
    def romanToInt(self, s):
        """
        :type s: str
        :rtype: int
        """
        d = {"I": 1, "V": 5, "X": 10, "L": 50, "C": 100, "D": 500, "M": 1000}
        num = 0
        c = 1
        for w in s[::-1]:
            if c <= d[w]:
                num += d[w]
                c = d[w]
            else:
                num -= d[w]

        return num
```
