## Remove Invalid Paranthesis

Remove the minimum number of invalid parentheses in order to make the input string valid. Return all possible results.

Note: The input string may contain letters other than the parentheses ( and ).

```
Examples:
"()())()" -> ["()()()", "(())()"]
"(a)())()" -> ["(a)()()", "(a())()"]
")(" -> [""]
```

### Solution

```java
public class Solution {
    public List<String> removeInvalidParentheses(String s) {
        List<String> res = new ArrayList<>();

        if(s == null) return res;

        Queue<String> q = new LinkedList<>();
        Set<String> visited = new HashSet<>();

        visited.add(s);
        q.add(s);

        boolean found = false;

        while(!q.isEmpty()) {
            s = q.poll();

            if(isValid(s)) {
                res.add(s);
                found = true;
            }

            if(found) continue;

            for(int i = 0;i<s.length();i++) {
                if(s.charAt(i) != '(' && s.charAt(i) != ')') continue;

                String t = s.substring(0, i) + s.substring(i+1);

                if(!visited.contains(t)) {
                    q.add(t);
                    visited.add(t);
                }
            }
        }

        return res;
    }

    boolean isValid(String s) {
        int count = 0;
        for(int i = 0;i<s.length();i++) {
            if(s.charAt(i) == '(')
                count += 1;
            if(s.charAt(i) == ')' && count-- == 0)
                return false;
        }

        return count == 0;
    }
}
```
