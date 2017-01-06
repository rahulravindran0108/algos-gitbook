## Decode Ways

A message containing letters from A-Z is being encoded to numbers using the following mapping:
```
'A' -> 1
'B' -> 2
...
'Z' -> 26
```

Given an encoded message containing digits, determine the total number of ways to decode it.

For example,
Given encoded message "12", it could be decoded as "AB" (1 2) or "L" (12).

The number of ways decoding "12" is 2.

### Solution

```python
class Solution(object):
    def numDecodings(self, s):
        """
        :type s: str
        :rtype: int
        """
        if s == "": return 0
        dp = [0 for x in range(len(s)+1)]
        dp[0] = 1
        for i in range(1, len(s) + 1):
            if s[i-1] != "0":
                dp[i] += dp[i - 1]
            if i != 1 and s[i-2:i] < "27" and s[i-2:i] > "09":
                dp[i] += dp[i-2]
        return dp[len(s)]
```

```java
public class Solution {
    public int numDecodings(String s) {
        if(s.length() == 0 || s == null) return 0;
        int [] dp = new int[s.length() + 1];
        dp[0] = 1;
        dp[1] = s.charAt(0) != '0' ? 1 : 0;
        for(int i = 2;i<=s.length();i++) {
            int first = Integer.valueOf(s.substring(i-1, i));
            int second = Integer.valueOf(s.substring(i-2, i));

            if(first >= 1 && first <= 9)
                dp[i] += dp[i-1];

            if(second >= 10 && second <= 26)
                dp[i] += dp[i-2];
        }

        return dp[s.length()];
    }
}
```
