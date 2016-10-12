## String Reduction (Hackerrank)

Given a string consisting of letters, 'a', 'b' and 'c', we can perform the following operation:

Take any two adjacent distinct characters and replace them with the third character.
For example, if 'a' and 'c' are adjacent, they can replaced by 'b'.

Find the smallest string which we can obtain by applying this operation repeatedly.

### Solution

```python
#!/usr/bin/py
# Head ends here

from collections import Counter

def stringReduction(a):
    c = Counter(a)
    if (c['a'] == 0 and c['b'] == 0) or (c['b'] == 0 and c['c'] == 0) or (c['a'] == 0 and c['c'] == 0):
        return len(a)
    elif (c['a'] %2 == 0 and c['b'] %2 == 0 and c['c'] %2 == 0) or (c['a'] %2 != 0 and c['b'] %2 != 0 and c['c'] %2 != 0):
        return 2
    else:
        return 1

# Tail starts here
if __name__ == '__main__':
    t = input()
    for i in range(0,t):
        a=raw_input()
        print stringReduction(a)
```
