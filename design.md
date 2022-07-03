### [剑指 Offer 59 - II. 队列的最大值](https://leetcode.cn/problems/dui-lie-de-zui-da-zhi-lcof/)

请定义一个队列并实现函数 `max_value` 得到队列里的最大值，要求函数`max_value`、`push_back` 和 `pop_front` 的**均摊**时间复杂度都是O(1)。

若队列为空，`pop_front` 和 `max_value` 需要返回 -1

**示例 1：**

> **输入:**
`["MaxQueue","push_back","push_back","max_value","pop_front","max_value"]`
`[[],[1],[2],[],[],[]]`
**输出:** `[null,null,null,2,1,2]`

**示例 2：**

> **输入:**
`["MaxQueue","pop_front","max_value"]`
`[[],[],[]]`
**输出:**`[null,-1,-1]`

```py
import queue
import collections

class MaxQueue:

    def __init__(self):
        self.queue = queue.Queue()
        self.deque = collections.deque()

    def max_value(self) -> int:
        if not self.deque:
            return -1
        return self.deque[0]


    def push_back(self, value: int) -> None:
        self.queue.put(value)
        while self.deque and self.deque[-1] < value:
            self.deque.pop()
        self.deque.append(value)


    def pop_front(self) -> int:
        #if self.queue.empty():
        if not self.deque:
            return -1
        x = self.queue.get()
        if x == self.deque[0]:
            self.deque.popleft()
        return x
```

```java
import java.util.Deque;
import java.util.LinkedList;
import java.util.Queue;

public class MaxQueue {

    Queue<Integer> queue;
    Deque<Integer> deque;

    public MaxQueue() {
        queue = new LinkedList<>();
        deque = new LinkedList<>();
    }

    public int max_value() {
        if (deque.isEmpty()){
            return -1;
        }
        return deque.peekFirst();
    }

    public void push_back(int value) {
        queue.offer(value);
        while (!deque.isEmpty() && value > deque.peekLast()){
            deque.pollLast();
        }
        deque.offerLast(value);
    }

    public int pop_front() {
        if (queue.isEmpty()){
            return -1;
        }
        int x = queue.poll();
        if (x == deque.peekFirst()){
            deque.pollFirst();
        }
        return x;
    }
}
```