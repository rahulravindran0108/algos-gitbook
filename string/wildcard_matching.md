## Wildcard Matching

Implement wildcard pattern matching with support for '?' and `'*'.`

```
'?' Matches any single character.
'*' Matches any sequence of characters (including the empty sequence).

The matching should cover the entire input string (not partial).

The function prototype should be:
bool isMatch(const char *s, const char *p)

Some examples:
isMatch("aa","a") → false
isMatch("aa","aa") → true
isMatch("aaa","aa") → false
isMatch("aa", "*") → true
isMatch("aa", "a*") → true
isMatch("ab", "?*") → true
isMatch("aab", "c*a*b") → false
```

### Solution

```java
public class Solution {
    public boolean isMatch(String s, String p) {
        int sdx = 0, pdx = 0, startIdx = -1, match = 0;

        while(sdx < s.length()) {
            if(pdx < p.length() && (p.charAt(pdx) == '?' || s.charAt(sdx) == p.charAt(pdx))) {
                pdx += 1;
                sdx += 1;
            } else if(pdx < p.length() && p.charAt(pdx) == '*') {
                startIdx = pdx;
                match = sdx;
                pdx += 1;
            } else if(startIdx != -1) {
                pdx = startIdx + 1; // reset pattern pointer
                sdx = ++match;
            } else return false;
        }

        while(pdx < p.length() && p.charAt(pdx) == '*')
            pdx += 1;

        return pdx == p.length();
    }
}
```
