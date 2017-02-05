## Least Frequently Used

Design and implement a data structure for Least Frequently Used (LFU) cache. It should support the following operations: get and put.

get(key) - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.
put(key, value) - Set or insert the value if the key is not already present. When the cache reaches its capacity, it should invalidate the least frequently used item before inserting a new item. For the purpose of this problem, when there is a tie (i.e., two or more keys that have the same frequency), the least recently used key would be evicted.

Follow up:
Could you do both operations in O(1) time complexity?

```
Example:

LFUCache cache = new LFUCache( 2 /* capacity */ );

cache.put(1, 1);
cache.put(2, 2);
cache.get(1);       // returns 1
cache.put(3, 3);    // evicts key 2
cache.get(2);       // returns -1 (not found)
cache.get(3);       // returns 3.
cache.put(4, 4);    // evicts key 1.
cache.get(1);       // returns -1 (not found)
cache.get(3);       // returns 3
cache.get(4);       // returns 4
```

### Solution

```python
class LFUCache(object):

    def __init__(self, capacity):
        """
        :type capacity: int
        """
        self.cache = dict()
        self.frequency = collections.defaultdict(collections.OrderedDict)
        self.volume = capacity
        self.least_freq = 0

    def get(self, key):
        """
        :type key: int
        :rtype: int
        """
        if key not in self.cache:
            return -1
        else:
            val, freq = self.cache[key]
            self.cache[key][1] += 1

            del self.frequency[freq][key]
            self.frequency[freq + 1][key] = 0
            if self.least_freq == freq and len(self.frequency[freq]) == 0:
                self.least_freq = freq + 1
            return val

    def put(self, key, value):
        """
        :type key: int
        :type value: int
        :rtype: void
        """
        if key in self.cache:
            # key is already present. update both cache and frequency table
            freq, val = self.cache[key]
            self.cache[key] = [value, freq + 1]
            del self.frequency[freq][key]
            self.frequency[freq + 1][key] = 0
            if self.least_freq == freq and len(self.frequency[freq]) == 0:
                self.least_freq = freq + 1
        else:
            if self.volume == 0:
                if len(self.frequency[self.least_freq]) > 0:
                    invalid = self.frequency[self.least_freq].keys()[0] # key of the invalid element.
                    self.frequency[self.least_freq].popitem(last = False)
                    del self.cache[invalid]
                    self.volume += 1
            if self.volume == 0:
                return

            self.cache[key] = [value,0]
            self.frequency[0][key]=0
            self.volume -=1
            self.least_freq = 0

# Your LFUCache object will be instantiated and called as such:
# obj = LFUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)
```
