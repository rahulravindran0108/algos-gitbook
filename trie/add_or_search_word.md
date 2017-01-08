## Add or Search Word

Design a data structure that supports the following two operations:
```
void addWord(word)
bool search(word)
```
search(word) can search a literal word or a regular expression string containing only letters a-z or .. A . means it can represent any one letter.

For example:
```
addWord("bad")
addWord("dad")
addWord("mad")
search("pad") -> false
search("bad") -> true
search(".ad") -> true
search("b..") -> true
```

Note:
You may assume that all words are consist of lowercase letters a-z.
### Solution

```python
class TrieNode:
    def __init__(self):
        self.childs = dict()
        self.isWord = False


class WordDictionary(object):
    def __init__(self):
        """
        initialize your data structure here.
        """
        self.root = TrieNode()


    def addWord(self, word):
        """
        Adds a word into the data structure.
        :type word: str
        :rtype: void
        """
        node = self.root
        for letter in word:
            child = node.childs.get(letter)
            if child is None:
                child = TrieNode()
                node.childs[letter] = child
            node = child
        node.isWord = True


    def search(self, word):
        """
        Returns if the word is in the data structure. A word could
        contain the dot character '.' to represent any one letter.
        :type word: str
        :rtype: bool
        """
        return self.find(self.root, word)

    def find(self, node, word):
        if word == '':
            return node.isWord
        if word[0] == '.':
            for x in node.childs:
                if self.find(node.childs[x], word[1:]):
                    return True
        else:
            child = node.childs.get(word[0])
            if child:
                return self.find(child, word[1:])
        return False


# Your WordDictionary object will be instantiated and called as such:
# wordDictionary = WordDictionary()
# wordDictionary.addWord("word")
# wordDictionary.search("pattern")
```

```java
public class WordDictionary {

    Map<Integer, List<String>> map = new HashMap<>();

    // Adds a word into the data structure.
    public void addWord(String word) {
        int index = word.length();

        if(!map.containsKey(index)) {
            List<String> lst = new ArrayList<>();
            lst.add(word);
            map.put(index, lst);
        } else {
            map.get(index).add(word);
        }
    }

    // Returns if the word is in the data structure. A word could
    // contain the dot character '.' to represent any one letter.
    public boolean search(String word) {
        int key = word.length();

        if(!map.containsKey(key))
            return false;

        List<String> lst = map.get(key);
        if(isWord(word))
            return lst.contains(word);

        for(String s : lst)
            if(isSame(s, word))
                return true;

        return false;
    }

    public boolean isWord(String s) {
        for(int i = 0;i<s.length();i++) {
            if(!Character.isLetter(s.charAt(i)))
                return false;
        }

        return true;
    }

    public boolean isSame(String s, String match) {
        if(s.length() != match.length())
            return false;

        for(int i = 0;i<s.length();i++) {
            if(match.charAt(i) != '.' && s.charAt(i) != match.charAt(i))
                return false;
        }

        return true;
    }
}

// Your WordDictionary object will be instantiated and called as such:
// WordDictionary wordDictionary = new WordDictionary();
// wordDictionary.addWord("word");
// wordDictionary.search("pattern");
```
