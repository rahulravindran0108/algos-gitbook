## Palindrome Pairs

Given a list of unique words, find all pairs of distinct indices (i, j) in the given list, so that the concatenation of the two words, i.e. words[i] + words[j] is a palindrome.

```
Example 1:
Given words = ["bat", "tab", "cat"]
Return [[0, 1], [1, 0]]
The palindromes are ["battab", "tabbat"]
```

```
Example 2:
Given words = ["abcd", "dcba", "lls", "s", "sssll"]
Return [[0, 1], [1, 0], [3, 2], [2, 4]]
The palindromes are ["dcbaabcd", "abcddcba", "slls", "llssssll"]
```

### Solution

```java
public class Solution {
    public List<List<Integer>> palindromePairs(String[] words) {
        List<List<Integer>> res = new ArrayList<>();
        if(words.length == 0)
            return res;

        Map<String, Integer> map = new HashMap<>();

        for(int i = 0; i < words.length; i++){
            map.put(words[i], i);
        }

        // look for ""
        if(map.containsKey("")) {
            int idx = map.get("");

            for(int i = 0;i<words.length;i++) {
                if(i == idx) continue;
                if(isPalindrome(words[i])) {
                    res.add(Arrays.asList(idx, i));
                    res.add(Arrays.asList(i, idx));
                }
            }
        }

        for(int i = 0;i<words.length;i++) {
            String rev = reverseString(words[i]);
            if(map.containsKey(rev)) {
                int idx = map.get(rev);
                if(idx == i) continue;
                res.add(Arrays.asList(i, idx));
            }
        }

        for(int i = 0;i<words.length;i++) {
            String cur = words[i];

            for(int cut = 1;cut<cur.length();cut++) {

                if(isPalindrome(cur.substring(0, cut))) {
                    String rev_cut = reverseString(cur.substring(cut));
                    if(map.containsKey(rev_cut)) {
                        int found = map.get(rev_cut);
                        if(found == i) continue;
                        res.add(Arrays.asList(found, i));
                    }
                }

                if(isPalindrome(cur.substring(cut))) {
                    String cut_r = reverseString(cur.substring(0, cut));
                    if(map.containsKey(cut_r)) {
                        int found = map.get(cut_r);
                        if(found == i) continue;
                        res.add(Arrays.asList(i, found));
                    }
                }

            }
        }


        return res;
    }

    public String reverseString(String str){
        StringBuilder sb= new StringBuilder(str);
        return sb.reverse().toString();
    }

    public boolean isPalindrome(String s) {
        int begin = 0, end = s.length() - 1;

        while(begin < end) {
            if(s.charAt(begin++) != s.charAt(end--))
                return false;
        }
        return true;
    }
}
```
