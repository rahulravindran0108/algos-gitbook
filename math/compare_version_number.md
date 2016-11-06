## Compare Version Number

### Solution

```python
class Solution(object):
    def compareVersion(self, version1, version2):
        """
        :type version1: str
        :type version2: str
        :rtype: int
        """
        v1 = list(map(int, version1.split(".")))
        v2 = list(map(int, version2.split(".")))
        size = max(len(v1), len(v2))

        for i in range(size):
            n1 = v1[i] if i < len(v1) else 0
            n2 = v2[i] if i < len(v2) else 0

            if n1 > n2:
                return 1
            if n1 < n2:
                return -1
        return 0
        
```
