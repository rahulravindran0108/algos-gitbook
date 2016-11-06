## Pascal Triangle

Given numRows, generate the first numRows of Pascal's triangle.

For example, given numRows = 5,
Return
```
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

### Solution

```python
class Solution(object):
    def generate(self, numRows):
        """
        :type numRows: int
        :rtype: List[List[int]]
        """
        if numRows == 0:
            return []
        row = [1]
        k = [0]
        result = [row]
        for i in range(0, numRows-1):
            row = [l+r for l,r in zip(row+k, k+row)]
            result.append(row)
        return result
```
