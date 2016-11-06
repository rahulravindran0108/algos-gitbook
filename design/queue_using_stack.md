## Queue using Stack

Implement the following operations of a queue using stacks.
```
push(x) -- Push element x to the back of queue.
pop() -- Removes the element from in front of queue.
peek() -- Get the front element.
empty() -- Return whether the queue is empty.
Notes:
You must use only standard operations of a stack -- which means only push to top, peek/pop from top, size, and is empty operations are valid.
Depending on your language, stack may not be supported natively. You may simulate a stack by using a list or deque (double-ended queue), as long as you use only standard operations of a stack.
You may assume that all operations are valid (for example, no pop or peek operations will be called on an empty queue).
```

### Solution

```python
class Queue(object):
    def __init__(self):
        """
        initialize your data structure here.
        """
        self.input = []
        self.output = []

    def push(self, x):
        """
        :type x: int
        :rtype: nothing
        """
        self.input.append(x)


    def pop(self):
        """
        :rtype: nothing
        """
        self.peek()
        return self.output.pop()

    def peek(self):
        """
        :rtype: int
        """
        if self.output == []:
            while self.input != []:
                self.output.append(self.input.pop())
        return self.output[-1]


    def empty(self):
        """
        :rtype: bool
        """
        return self.input == [] and self.output == []
```
