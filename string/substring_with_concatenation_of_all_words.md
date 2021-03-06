## Substring with Concatenation of All Words

You are given a string, s, and a list of words, words, that are all of the same length. Find all starting indices of substring(s) in s that is a concatenation of each word in words exactly once and without any intervening characters.

For example, given:
```
s: "barfoothefoobarman"
words: ["foo", "bar"]
```

You should return the indices: [0,9].
(order does not matter).

### Solution

```python
from collections import defaultdict

class Solution(object):
    def findSubstring(self, s, words):
        """
        :type s: str
        :type words: List[str]
        :rtype: List[int]
        """
        result, n_word, l_word  = [], len(words), len(words[0])
        word_map = defaultdict(int)

        for i in words:
            word_map[i] += 1

        for i in range((len(s) + 1) - n_word * l_word):
            cur, j, = defaultdict(int), 0
            while j < n_word:
                word = s[i + j * l_word: i + j * l_word + l_word]
                if word not in word_map:
                    break
                cur[word] += 1
                if cur[word] > word_map[word]:
                    break
                j += 1
            if j == n_word:
                result.append(i)
        return result
```

```java
public class Solution {
    public List<Integer> findSubstring(String s, String[] words) {
        List<Integer> res = new ArrayList<>();

        if(s == null || words == null || words.length == 0) return res;
        int len = words[0].length();

        Map<String, Integer> map = new HashMap<>();
        for(String word : words)
            map.put(word, map.containsKey(word) ? map.get(word) + 1 : 1);

        for(int i = 0;i <= s.length() - len * words.length;i++) {
            Map<String, Integer> copy = new HashMap<>(map);

            for(int j = 0;j<words.length;j++) {
                String cur = s.substring(i + j * len, i + j* len + len);

                if(copy.containsKey(cur)) {
                    int count = copy.get(cur);

                    if(count == 1) copy.remove(cur);
                    else copy.put(cur, count - 1);

                    if(copy.isEmpty()) {
                        res.add(i);
                        break;
                    }
                } else break;
            }
        }

        return res;
    }
}
```
