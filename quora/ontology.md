## Ontology

Quora has many questions on different topics, and a common product use-case for our @mention selectors and search service is to look-up questions under a certain topic as quickly as possible.

For this problem, imagine a simplified version of Quora where each question has only one topic associated with it. In turn, the topics form a simplified
ontology where each topic has a list of children, and all topics are descendants of a single root topic.

Design a system that allows for fast searches of questions under topics. There are NN topics, MM questions, and KK queries, given in this order. Each query has a desired topic as well as a desired string prefix. For each query, return the number of questions that fall under the queried topic and begin with the desired string. When considering topics, we want to include all descendants of the queried topic as well as the queried topic itself. In other words, each query searches over the subtree of the topic.

The topic ontology is given in the form of a flattened tree of topic names, where each topic may optionally have children. If a topic has children, they are listed after it within parentheses, and those topics may have children of their own, etc. See the sample for the exact input format. The tree is guaranteed to have a single root topic.

For ease of parsing, each topic name will be composed of English alphabetical characters, and each question and query text will be composed of English alphabetical characters, spaces, and question marks. Each question and query text will be well behaved: there will be no consecutive spaces or leading/trailing spaces. All queries, however, are case sensitive.

Constraints
For 100% of the test data, 1≤N,M,K≤1051≤N,M,K≤105 and the input file is smaller than 5MB
For 50% of the test data, 1≤N,M,K≤2⋅1041≤N,M,K≤2⋅104 and the input file is smaller than 1MB

Input Format
Line 1: One integer NN
Line 2: NN topics arranged in a flat tree (see sample)
Line 3: One integer MM
Line 4...M+3: Each line contains a topic name, followed by a colon and a space, and then the question text.
Line M+4: One integer KK
Line M+5...M+K+4: Each line contains a topic name, followed by a space, and then the query text.

Output Format
Line 1...K: Line ii should contain the answer for the iith query.

Sample Input
```
6
Animals ( Reptiles Birds ( Eagles Pigeons Crows ) )
5
Reptiles: Why are many reptiles green?
Birds: How do birds fly?
Eagles: How endangered are eagles?
Pigeons: Where in the world are pigeons most densely populated?
Eagles: Where do most eagles live?
4
Eagles How en
Birds Where
Reptiles Why do
Animals Wh
```

Sample Output
```
1
2
0
3
```

### Solution

```python
from collections import deque


class TrieNode:
    def __init__(self):
        self.count = 0
        self.children = {}


class Trie:
    def __init__(self):
        self.head = TrieNode()

    def insert(self, sentence):
        """
        Insert sentence into Trie.

        Args:
            sentence: sentence to be inserted into Trie
        Returns:
            None
        """
        current = self.head
        for char in sentence:
            if char in current.children:
                current.children[char].count += 1
            else:
                current.children[char] = TrieNode()
                current.children[char].count = 1
            current = current.children[char]

    def return_query_count(self, query):
        """
        Return Query Count.
        Args:
            query: query entered by user.
        Returns:
            number of relevant queries
        """
        current = self.head
        try:
            for char in query:
                current = current.children[char]
            return current.count
        except KeyError:
            return 0


class TreeNode:
    def __init__(self):
        self.trie = Trie()
        self.children = []


class Tree:
    def __init__(self):
        self.map = {}

    def insert_node(self, root, children):
        """Insert the tree node."""
        if root not in self.map:
            self.map[root] = TreeNode()
        self.map[root].children += children

    def insert_sentence(self, node, sentence):
        """Insert sentence into Trie."""
        self.map[node].trie.insert(sentence)

    def query(self, node, query):
        """Get query count."""
        return self.map[node].trie.return_query_count(query)


class Ontology:
    def __init__(self):
        """Constructor"""
        self.tree = Tree()

    def build_query(self, query):
        """
        Save query into tree.
        Args:
            query: string representing the query to save
        Returns:
            None
        Raises:
            Value Error in case the query is malformed.
        """
        try:
            node, sentence = query.split(":")
            self.tree.insert_sentence(node.strip(), sentence.strip())
        except ValueError:
            return ValueError("Not a valid query")

    def parse_flat_tree(self, ps):
        """
        Parse the flat tree.
        Args:
            parse_string: string containing the flat tree
        Returns:
            Ontology Structure
        """
        words = deque(ps.split(" "))
        try:
            root = words.popleft()
            if words.popleft() == "(":
                self.parse_recurse(root, words)
        except IndexError:
            return IndexError("No ")

    def parse_recurse(self, root, words):
        """
        Recursively build the Tree.
        Args:
            root: current parent to add children too.
            words: queue containing tokens of query
        Returns:
            None
        Raises:
            IndexError
        """
        child, children, previous_root = words.popleft(), [], None
        while child:
            if child == "(":
                self.parse_recurse(previous_root, words)
                child = words.popleft()
            elif child == ")":
                if len(children) > 0:
                    self.tree.insert_node(root, children)
                break
            else:
                children.append(child)
                self.tree.insert_node(child, [])
                previous_root = child
                try:
                    child = words.popleft()
                except IndexError:
                    child = None

    def get_query_count(self, query):
        """
        Get query count.
        Args:
            query: query to get count of matching questions
        Returns:
            count of related topics to query
        """
        try:
            head, sep, query = query.partition(" ")
        except ValueError:
            return ValueError("Not a valid query to match")
        queue, count = deque(), 0
        queue.append(head)
        while queue:
            current = queue.popleft()
            try:
                queue.extend(self.tree.map[current].children)
            except KeyError:
                return 0
            count += self.tree.query(current, query)
        return count


def main():
    o = Ontology()
    n_topics = int(raw_input())
    flat_tree = raw_input()
    o.parse_flat_tree(flat_tree)

    n_query = int(raw_input())
    for i in xrange(n_query):
        o.build_query(raw_input())

    n_match_query = int(raw_input())
    for i in xrange(n_match_query):
        print o.get_query_count(raw_input())

if __name__ == '__main__':
    main()

```
