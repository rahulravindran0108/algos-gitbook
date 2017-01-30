## Text Justification

Given an array of words and a length L, format the text such that each line has exactly L characters and is fully (left and right) justified.

You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces ' ' when necessary so that each line has exactly L characters.

Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line do not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.

For the last line of text, it should be left justified and no extra space is inserted between words.

```
For example,
words: ["This", "is", "an", "example", "of", "text", "justification."]
L: 16.

Return the formatted lines as:
[
   "This    is    an",
   "example  of text",
   "justification.  "
]
```

Note: Each word is guaranteed not to exceed L in length.

### Solution

```java
public class Solution {
    public List<String> fullJustify(String[] words, int L) {
        List<String> res = new ArrayList<>();
        int idx  = 0;

        while(idx < words.length) {

            int count = words[idx].length(), last = idx + 1;

            while(last < words.length) {
                if (words[last].length() + count + 1 > L) break;
                count += words[last].length() + 1;
                last++;
            }

            int diff = last - idx - 1;
            StringBuilder sb = new StringBuilder();

            if(diff == 0 || last == words.length) {
                for (int i = idx; i < last; i++) {
                    sb.append(words[i] + " ");
                }

                sb.deleteCharAt(sb.length() - 1);
                for (int i = sb.length(); i < L; i++) {
                    sb.append(" ");
                }
            } else {
                int spaces = (L - count) / diff;

                int remainder = (L - count) % diff;

                for(int i = idx;i<last;i++) {
                    sb.append(words[i]);

                    if (i < last - 1) {
                        for (int j = 0; j <= (spaces + ((i - idx) < remainder ? 1 : 0)); j++) {
                            sb.append(" ");
                        }
                    }
                }
            }

            res.add(sb.toString());
            idx = last;
        }

        return res;
    }
}
```
