## Bigger is Better

Given a word w, rearrange the letters of w to construct another word s in such a way that s is lexicographically greater than w. In case of multiple possible answers, find the lexicographically smallest one among them.

### Solution

```python
# Enter your code here. Read input from STDIN. Print output to STDOUT
t = int(raw_input())
for i in range(t):
    s = list(raw_input().strip())
    start = -1
    for i in range(len(s) - 1):
        if s[i] < s[i+1]:
            start = i

    if start == -1:
        print "no answer"
        continue

    end = -1
    for j in range(start+1, len(s)):
        if s[start] < s[j]:
            end = j
    s[start], s[end] = s[end], s[start]

    a = s[start+1:]
    a.sort()

    for j in range(start+1, len(nums)):
        s[j] = a[j - start - 1]
    print "".join(s)

```
