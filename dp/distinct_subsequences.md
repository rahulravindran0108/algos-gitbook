## Distinct Subsequences

Given a string S and a string T, count the number of distinct subsequences of T in S.

A subsequence of a string is a new string which is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (ie, "ACE" is a subsequence of "ABCDE" while "AEC" is not).

Here is an example:
`S = "rabbbit", T = "rabbit"`

Return 3.

### Solution

```python
class Solution(object):
    def numDistinct(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: int
        """
        m, n = len(s) + 1, len(t) + 1
        dp = [[0 for _ in range(n)] for _ in range(m)]

        for i in range(m):
            dp[i][0] = 1

        for i in range(1,m):
            for j in range(1,n):
                if s[i-1] == t[j-1]:
                    dp[i][j] = dp[i-1][j] + dp[i-1][j-1]
                else:
                    dp[i][j] = dp[i-1][j]

        return dp[m-1][n-1]


```
