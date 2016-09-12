## Labeller

In Progress

### Solution

```python
import numpy

from collections import Counter
from nltk import word_tokenize
from nltk.corpus.reader.wordnet import NOUN
from nltk.stem import WordNetLemmatizer

class Question:
    def __init__(self):
        self.category_count = None  # used to store the top topics
        self.categories = []
        self.map = {}
        self.tf = {}
        self.context_matrix = {}

    def insert_words_and_categories(self, words, categories):
        """
        Args:
            words: set of words that are already cleaned.
        Returns:
            None
        """
        self.categories.extend(categories)
        for word in words:
            if word in self.map:
                self.map[word].extend(categories)
                self.map[word] = list(set(self.map[word]))
            else:
                self.map[word] = list(categories)
        self.update_context_matrix(categories)

    def build_top_topics(self):
        """Builds the counter for top topics."""
        self.category_count = Counter(self.categories)

    def update_context_matrix(self, categories):
        """
        Update the co-occurance matrix for all the words.
        """
        for i in xrange(len(categories)):
            if categories[i] in self.context_matrix:
                self.context_matrix[categories[i]].update(categories[i+1:])
                self.context_matrix[categories[i]].update(categories[i-1:0:-1])
            else:
                self.context_matrix[categories[i]] = Counter(categories[i+1:])
                self.context_matrix[categories[i]].update(categories[i-1:0:-1])


class Labeler:
    def __init__(self):
        self.stop_words = ['all', 'just', 'being', 'over', 'both', 'through',
                           'its', 'before', 'herself', 'had', 'should', 'them',
                           'only', 'won', 'under', 'ours', 'has', 'then', 'to',
                           'his', 'very', 'they', 'not', 'during', 'him',
                           'nor', 'd', 'did', 'these', 'she', 'each', 'now',
                           'further', 'where', 'because', 'doing', 'are',
                           'our', 'ourselves', 'out', 'what', 'for', 'below',
                           'does', 'above', 'some', 'few', 'between', 'be',
                           'we', 'after', 'here', 'by', 'on', 'about', 'of',
                           'against', 's', 'or', 'own', 'into', 'yourself',
                           'down', 'your', 'from', 'her', 'whom', 'there',
                           'been', 'their', 'too', 'themselves', 'was',
                           'until', 'more', 'himself', 'that', 'but', 'with',
                           'than', 'those', 'he', 'me', 'myself', 'this', 'up',
                           'will', 'while', 'can', 'were', 'my', 'and', 'do',
                           'is', 'am', 'it', 'an', 'as', 'itself', 'at',
                           'have', 'in', 'any', 'if', 'again', 'no', 'when',
                           'same', 'how', 'other', 'which', 'you', 'who',
                           'most', 'such', 'why', 'a', 'off', 'i', 'm', 'so',
                           'y', 'the', 'having', 'once', 'yours', "'s", '?',
                           'i', 'me', 'my', 'myself', 'we', 'our', 'ours',
                           'ourselves', 'yo', 'your', 'yours', 'yourself',
                           'yourselves', 'he', 'him', 'his', 'himself', 'she',
                           'her', 'hers', 'herself', 'it', 'its', 'itself',
                           'they', 'them', 'their', 'theirs', 'themselves',
                           'what', 'which', 'who', 'whom', 'this', 'that',
                           'these', 'those', 'am', 'is', 'are', 'was', 'were',
                           'be', 'been', 'have', 'has', 'had', 'having', 'do',
                           'does', 'did', 'doing', 'a', 'an', 'the', 'and',
                           'but', 'if', 'or', 'because', 'as', 'until',
                           'of', 'at', 'by', 'for', 'with', 'about', 'against',
                           'between', 'into', 'through', 'during', 'before',
                           'after', 'above', 'below', 'to', 'from', 'up',
                           'down', 'in', 'out', 'on', 'off', 'under',
                           'again', 'further', 'then', 'once', 'here', 'there',
                           'when', 'where', 'why', 'how', 'any', 'both',
                           'each', 'few', 'more', 'most', 'other', 'some',
                           'such', 'no', 'nor', 'not', 'only', 'own', 'same',
                           'so', 'than', 'too', 'very', 's', 't', 'can',
                           'will', 'don', 'should', 'now', 'while', 'How', 'In']
        self.q = Question()
        self.wnl = WordNetLemmatizer()

    def tokenize_and_build(self, sentence, categories):
        """
        Tokenize the sentence and build the resultant data structure.

        Args:
            sentence: string representing the sentence to enter
        Returns:
            None
        Raises:
            None
        """
        tokens = word_tokenize(sentence)
        words = [self.wnl.lemmatize(word, NOUN) for word in tokens if word not in self.stop_words]
        self.q.insert_words_and_categories(words, categories)
        self.q.update_context_matrix(categories)

    def query_new_questions(self, sentence):
        """
        """
        tokens = word_tokenize(sentence)
        words = [self.wnl.lemmatize(word, NOUN) for word in tokens if word not in self.stop_words]
        categories = []
        for word in words:
            if word in self.q.map:
                if not categories:
                    categories.extend(self.q.map[word])
                else:
                    categories.extend(self.q.map[word])
        answer = []
        for k, v in Counter(categories).most_common(10):
            answer.append(k)
        return " ".join(str(x) for x in answer)


def main():
    l = Labeler()
    with open("labeler_sample.in", "r") as f:
        content = f.readlines()
    n, m = map(int, content[0].split(" "))
    for j in range(1, 2 * n, 2*n+m):
        categories = map(int, content[j].split(" "))
        sentence = content[j+1].strip()
        l.tokenize_and_build(sentence, categories)
    l.q.build_top_topics()
    results = []

    for i in range(2*n, 2*n+1):
        results.append(l.query_new_questions(content[i].strip()))
    with open("my_answers.txt", "wb") as f:
        f.write("\n".join(results))

if __name__ == '__main__':
    main()
```
