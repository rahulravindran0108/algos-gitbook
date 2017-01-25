## Repeated Substring Pattern

Given a non-empty string check if it can be constructed by taking a substring of it and appending multiple copies of the substring together. You may assume the given string consists of lowercase English letters only and its length will not exceed 10000.

```
Example 1:
Input: "abab"

Output: True
```

Explanation: It's the substring "ab" twice.

```
Example 2:
Input: "aba"

Output: False
Example 3:
Input: "abcabcabcabc"

Output: True
```

Explanation: It's the substring "abc" four times. (And the substring "abcabc" twice.)

### Solution

```java
public class Solution {
    public boolean repeatedSubstringPattern(String str) {
        int l = str.length();

        for(int i = l/2;i>=1;i--) {
            if(l % i == 0) {
                int m = l/i;

                String subS = str.substring(0,i);
    			StringBuilder sb = new StringBuilder();
    			for(int j=0;j<m;j++) {
    				sb.append(subS);
    			}

                if(sb.toString().equals(str)) return true;
            }
        }

        return false;
    }
}
```
