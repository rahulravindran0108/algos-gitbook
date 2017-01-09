## Word Break 2

Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, add spaces in s to construct a sentence where each word is a valid dictionary word. You may assume the dictionary does not contain duplicate words.

Return all such possible sentences.

For example, given
s = "catsanddog",
dict = ["cat", "cats", "and", "sand", "dog"].

A solution is ["cats and dog", "cat sand dog"].

### Solution

```java
public class Solution {
    public List<String> wordBreak(String s, List<String> wordDict) {
        return dfs(s, new HashMap<String, LinkedList<String>>(), wordDict);
    }

    public List<String> dfs(String s, HashMap<String, LinkedList<String>>map, List<String> wordDict) {
        // base case
        if(map.containsKey(s))
            return map.get(s);

        LinkedList<String> res = new LinkedList<>();

        if(s.length() == 0) {
            res.add("");
            return res;
        }

        for(String word : wordDict) {
            if(s.startsWith(word)) {
                List<String> subList = dfs(s.substring(word.length()), map, wordDict);
                for(String sub : subList)
                    res.add(word + (sub.isEmpty() ? "" : " ") + sub);
            }
        }
        map.put(s, res);
        return res;
    }
}
```
