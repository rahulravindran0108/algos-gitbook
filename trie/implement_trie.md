## Implement Trie

Implement a trie with insert, search, and startsWith methods.

Note:
You may assume that all inputs are consist of lowercase letters a-z.

### Solution

```python
class TrieNode(object):
    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.children = dict()
        self.is_word = False


class Trie(object):

    def __init__(self):
        self.root = TrieNode()

    def insert(self, word):
        """
        Inserts a word into the trie.
        :type word: str
        :rtype: void
        """
        node = self.root
        for letter in word:
            child = node.children.get(letter)
            if child is None:
                child = TrieNode()
                node.children[letter] = child
            node = child
        node.is_word = True

    def search(self, word):
        """
        Returns if the word is in the trie.
        :type word: str
        :rtype: bool
        """
        node = self.root
        for letter in word:
            node = node.children.get(letter)
            if node is None:
                return False
        return node.is_word

    def startsWith(self, prefix):
        """
        Returns if there is any word in the trie
        that starts with the given prefix.
        :type prefix: str
        :rtype: bool
        """
        node = self.root
        for letter in prefix:
          node = node.children.get(letter)
          if node is None:
            return False
        return True


# Your Trie object will be instantiated and called as such:
# trie = Trie()
# trie.insert("somestring")
# trie.search("key")
```

```java
class TrieNode {

    private final int R = 26;
    private final TrieNode [] children;
    private String item;

    // Initialize your data structure here.
    public TrieNode() {
        children = new TrieNode[R];
        item = "";        
    }

    public TrieNode [] getChildren() {
        return this.children;
    }

    public String getItem() {
        return this.item;
    }

    public void setItem(String item) {
        this.item = item;
    }

    public void setChild(int i, TrieNode n) {
        if(i >= 26 || i < 0) throw new IllegalArgumentException();
        this.children[i] = n;
    }

    public TrieNode getChild(int i) {
        if(i >= 26 || i < 0) throw new IllegalArgumentException();
        return this.children[i];
    }
}

public class Trie {
    private TrieNode root;

    public Trie() {
        root = new TrieNode();
    }

    // Inserts a word into the trie.
    public void insert(String word) {
        TrieNode cur = root;

        for(char c : word.toCharArray()) {
            if(cur.getChild(c - 'a') == null)
                cur.setChild(c - 'a', new TrieNode());
            cur = cur.getChild(c - 'a');
        }
        cur.setItem(word);
    }

    // Returns if the word is in the trie.
    public boolean search(String word) {
        TrieNode cur = root;
        for(char c : word.toCharArray()) {
            if(cur.getChild(c - 'a') == null) return false;
            cur = cur.getChild(c - 'a');
        }

        return cur.getItem().equals(word);
    }

    // Returns if there is any word in the trie
    // that starts with the given prefix.
    public boolean startsWith(String prefix) {
        TrieNode cur = root;
        for(char c : prefix.toCharArray()) {
            System.out.println(c);
            if(cur.getChild(c - 'a') == null)
                return false;

            cur = cur.getChild(c - 'a');
        }

        return true;
    }
}

// Your Trie object will be instantiated and called as such:
// Trie trie = new Trie();
// trie.insert("somestring");
// trie.search("key");
```
