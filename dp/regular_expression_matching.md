## Regular Expression Matching

Implement regular expression matching with support for `'.'` and `'*'`.

```
'.' Matches any single character.
'*' Matches zero or more of the preceding element.

The matching should cover the entire input string (not partial).

The function prototype should be:
bool isMatch(const char *s, const char *p)

Some examples:
isMatch("aa","a") → false
isMatch("aa","aa") → true
isMatch("aaa","aa") → false
isMatch("aa", "a*") → true
isMatch("aa", ".*") → true
isMatch("ab", ".*") → true
isMatch("aab", "c*a*b") → true
```

### Solution

```java
public class Solution {
    public boolean isMatch(String s, String p) {
        if(s == null || p == null) return false;
        int m = s.length(), n = p.length();

        boolean [][] dp = new boolean[m + 1][n + 1];

        dp[0][0] = true;
        for (int i = 0; i < p.length(); i++) {
            if (p.charAt(i) == '*' && dp[0][i-1]) {
                dp[0][i+1] = true;
            }
        }

        for(int i = 0;i<m;i++)
            for(int j = 0;j<n;j++) {

                if(p.charAt(j) == '.')
                    dp[i+1][j+1] = dp[i][j];
                if(p.charAt(j) == s.charAt(i))
                    dp[i+1][j+1] = dp[i][j];
                if(p.charAt(j) == '*') {
                    if(p.charAt(j - 1) != '.' && p.charAt(j - 1) != s.charAt(i))
                        dp[i+1][j+1] = dp[i + 1][j-1];
                    else
                        dp[i + 1][j + 1] = (dp[i+1][j] || dp[i][j+1] || dp[i+1][j-1]);
                }
            }

        return dp[s.length()][p.length()];
    }
}
```
