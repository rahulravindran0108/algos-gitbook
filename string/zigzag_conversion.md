## Zigzag Conversion
The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)
```
P   A   H   N
A P L S I I G
Y   I   R
```
And then read line by line: `"PAHNAPLSIIGYIR"`
Write the code that will take a string and make this conversion given a number of rows:

`string convert(string text, int nRows);`

convert("PAYPALISHIRING", 3) should return "PAHNAPLSIIGYIR".

### Solution

```python
class Solution(object):
    def convert(self, s, numRows):
        """
        :type s: str
        :type numRows: int
        :rtype: str
        """
        if numRows == 1:
            return s

        result = [[] for _ in range(numRows)]
        k = 2 * numRows - 2

        for idx, value in enumerate(s):
            pos = min(idx % k, k - idx % k)
            result[pos].append(value)
        r_str = ""
        for row in result:
            r_str+=''.join(row)
        return r_str
```
