## Pascal Triangle 2

Given an index k, return the kth row of the Pascal's triangle.

For example, given k = 3,
Return `[1,3,3,1].`

### Solution

```python
class Solution(object):
    def getRow(self, rowIndex):
        """
        :type rowIndex: int
        :rtype: List[int]
        """
        if rowIndex == 0:
            return [1]
        row = [1]
        k = [0]
        result = [row]
        for i in range(0, rowIndex):
            row = [l+r for l,r in zip(row+k, k+row)]
        return row
```
