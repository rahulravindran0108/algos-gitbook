## Spiral Matrix

Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

For example,
Given the following matrix:
```
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
You should return [1,2,3,6,9,8,7,4,5].
```

### Solution

```python
class Solution(object):
    def spiralOrder(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: List[int]
        """
        res = []
        if not matrix:
            return res
        i, j, di, dj = 0, 0, 0, 1
        m, n  = len(matrix), len(matrix[0])

        for x in range(m * n):
            res.append(matrix[i][j])
            matrix[i][j] = ""
            if matrix[(i + di) % m][(j + dj) % n] == "":
                di, dj = dj, -di
            i += di
            j += dj
        return res
```

```java
public class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {

        List<Integer> result = new ArrayList<>();
        if(matrix.length == 0) return result;

        int rowBegin = 0;
        int rowEnd = matrix.length-1;
        int colBegin = 0;
        int colEnd = matrix[0].length - 1;

        while(rowBegin <= rowEnd && colBegin <= colEnd) {
            // traverse right
            for(int i = colBegin;i<=colEnd;i++)
                result.add(matrix[rowBegin][i]);
            rowBegin++;

            // traverse down
            for(int i = rowBegin;i<=rowEnd;i++)
                result.add(matrix[i][colEnd]);

            colEnd--;

            // traverse left
            if(rowBegin <= rowEnd) {
                for(int i = colEnd;i>=colBegin;i--)
                    result.add(matrix[rowEnd][i]);

                rowEnd--;
            }

            // traverse up
            if(colBegin <= colEnd) {
                for(int i = rowEnd;i>=rowBegin;i--)
                    result.add(matrix[i][colBegin]);

                colBegin++;
            }
        }

        return result;



    }
}
```
