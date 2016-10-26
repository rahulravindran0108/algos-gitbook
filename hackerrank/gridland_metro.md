## Gridland Metro

The city of Gridland is represented as an  matrix where the rows are numbered from  to  and the columns are numbered from  to .

Gridland has a network of train tracks that always run in straight horizontal lines along a row. In other words, the start and end points of a train track are  and , where  represents the row number,  represents the starting column, and  represents the ending column of the train track.

The mayor of Gridland is surveying the city to determine the number of locations where lampposts can be placed. A lamppost can be placed in any cell that is not occupied by a train track.

Given a map of Gridland and its  train tracks, find and print the number of cells where the mayor can place lampposts.

### Solution


```python
from collections import defaultdict

def merge_overlap(ar):
    ar = sorted(ar)
    i = 1
    while i<=len(ar)-1:
        if ar[i][0] <= ar[i-1][1]:
            if ar[i][1] > ar[i-1][1]:
                ar[i-1][1] = ar[i][1]
            del ar[i]
            continue
        i+=1
    return sum([x2-x1+1 for x1,x2 in ar])

m,n,k = map(int, raw_input().strip().split(' '))


d = defaultdict(list)
for _ in range(k):
    r,c1,c2 = map(int, raw_input().strip().split(' '))
    d[r].append([c1,c2])


result = m*n    
for k in d:
    result -= merge_overlap(d[k])

print result
```
