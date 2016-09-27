## Merge Two Sorted List in Constant space

Merge Two Sorted List into one with the use of constant space.

Example:
```
Input: ar1[] = {1, 5, 9, 10, 15, 20};
       ar2[] = {2, 3, 8, 13};
Output: ar1[] = {1, 2, 3, 5, 8, 9}
        ar2[] = {10, 13, 15, 20}  
```

In this solution, I have hard coded the input. The important catch to this problem is that you have to do an insertion sort making the complexity O(m*n)

### Solution

```python
def main(a, b):
    m, n = len(a) - 1, len(b) - 1
    print m, n
    for i in range(n, -1, -1):
        j, last = m - 1, a[-1]
        while j >= 0 and a[j] > b[i]:
            a[j+1] = a[j]
            j -= 1
        if j != m-1:
            a[j+1] = b[i]
            b[i] = last
    print a, b

if __name__ == '__main__':
    a, b = [1, 5, 9, 10, 15, 20],  [2, 3, 8, 13]
    main(a, b)
```
