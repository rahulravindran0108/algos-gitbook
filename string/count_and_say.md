## Count and Say


### Solution

```java
public class Solution {
    public String countAndSay(int n) {

        StringBuilder cur = new StringBuilder("1"), prev;
        int count;
        char say;

        for(int i = 1;i<n;i++) {
            prev = cur;
            cur = new StringBuilder();

            say = prev.charAt(0);
            count = 1;

            for(int j = 1;j<prev.length();j++) {
                if(prev.charAt(j) != say) {
                    cur.append(count).append(say);
                    count = 1;
                    say = prev.charAt(j);
                }
                else
                    count ++;
            }

            cur.append(count).append(say);
        }

        return cur.toString();
    }
}
```
