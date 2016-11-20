## Game of Thrones - 1

Dothraki are planning an attack to usurp King Robert's throne. King Robert learns of this conspiracy from Raven and plans to lock the single door through which the enemy can enter his kingdom.

```
Sample Input : 01

aaabbbb
Sample Output : 01

YES
```

### Solution

```python
from collections import Counter

s = raw_input()
c = Counter(s)

nodd= len(filter(lambda x:x%2==1, c.values()))
print ["NO", "YES"][nodd <= 1]
```
