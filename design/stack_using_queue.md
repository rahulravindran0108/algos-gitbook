## Stack Using Queue

Implement the following operations of a stack using queues.

- push(x) -- Push element x onto stack.
- pop() -- Removes the element on top of the stack.
- top() -- Get the top element.
- empty() -- Return whether the stack is empty.

Notes:
You must use only standard operations of a queue -- which means only push to back, peek/pop from front, size, and is empty operations are valid.

Depending on your language, queue may not be supported natively. You may simulate a queue by using a list or deque (double-ended queue), as long as you use only standard operations of a queue.
You may assume that all operations are valid (for example, no pop or top operations will be called on an empty stack).


### Solution

```python
class Stack(object):
    def __init__(self):
        """
        initialize your data structure here.
        """
        self._queue = collections.deque()

    def push(self, x):
        """
        :type x: int
        :rtype: nothing
        """
        q = self._queue
        q.append(x)
        for _ in range(len(q) - 1):
            q.append(q.popleft())


    def pop(self):
        """
        :rtype: nothing
        """
        return self._queue.popleft()


    def top(self):
        """
        :rtype: int
        """
        return self._queue[0]


    def empty(self):
        """
        :rtype: bool
        """
        return not len(self._queue)
```
