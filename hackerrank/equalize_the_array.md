## Equalize the Array

Karl has an array of n integers defined as A = a0, a1 ... an. In one operation, he can delete any element from the array.

Karl wants all the elements of the array to be equal to one another. To do this, he must delete zero or more elements from the array. Find and print the minimum number of deletion operations Karl must perform so that all the array's elements are equal.

### Solution

```python
# Enter your code here. Read input from STDIN. Print output to STDOUT
from collections import Counter

_ = raw_input()
arr = map(int, raw_input().strip().split())
c = Counter(arr)
mc = c.most_common(1)

print len(arr) - mc[0][1]
```
