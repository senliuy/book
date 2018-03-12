# Q232. Implement Queue using Stacks

直达: [https://leetcode.com/problems/implement-queue-using-stacks/description/](https://leetcode.com/problems/implement-queue-using-stacks/description/)

Implement the following operations of a queue using stacks.

* push\(x\) -- Push element x to the back of queue.
* pop\(\) -- Removes the element from in front of queue.
* peek\(\) -- Get the front element.
* empty\(\) -- Return whether the queue is empty.

**Notes:**

* You must use
  only
  standard operations of a stack -- which means only
  `push to top`,`peek/pop from top`,`size`, and`is empty`
  operations are valid.
* Depending on your language, stack may not be supported natively. You may simulate a stack by using a list or deque \(double-ended queue\), as long as you use only standard operations of a stack.
* You may assume that all operations are valid \(for example, no pop or peek operations will be called on an empty queue\).

## 分析：

堆栈的操作顺序是先进后出，而队列是先进先出，如果要用堆栈实现队列，要在push, pop, top和empty四个操作中满足满足队列的先进先出的顺序

pop

举个例子，队列中先后插入了3个元素a,b,c, 首先我们把它们都存到栈stk1中，此时若要弹出一个数，按照堆栈的先进后出的顺序，应该弹出c，而队列的弹出应该是a。这时候，堆栈stk2就可以起作用了，我们将stk1的所有元素全部移动到stk2中，这时候再从stk2中弹出栈顶元素即可。

```
stk1: 
stk2: c,b
```

而插入的时候我们只需要将要插入的元素直接插入到stk1，看看能否只在push操作中移动堆栈元素。继续上面的例子，此时来了一个新的元素d，插入到stk1中。当要弹出元素时，由于剩下的元素中b是先来的，所以直接弹出b的栈顶元素即可，不需要移动stk1的元素，只有当stk2中为空时，才需要将stk1的元素移动到stk2中。

```
stk1: d
stk2: c,b
```

总结：

如果stk2为空，则将stk1的所有元素移动到stk2中，并弹出stk2的栈顶元素

如果stk2不为空，则直接弹出stk2的栈顶元素

push

插入到stk1中，不需要任何其他操作

top

类似pop操作，只是不弹出stk2的栈顶元素，只需要返回栈顶值即可

empty

stk1和stk2都为空，则队列为空

C++代码

```cpp
class MyQueue {
    stack<int> stk1;
    stack<int> stk2;
public:
    /** Initialize your data structure here. */
    MyQueue() {
    }

    /** Push element x to the back of queue. */
    void push(int x) {
        stk1.push(x);
    }

    /** Removes the element from in front of queue and returns that element. */
    int pop() {
        int res = peek();
        stk2.pop();
        return res;
    }

    /** Get the front element. */
    int peek() {
       if(!stk2.empty()){
            return stk2.top();
        }else{
            while(!stk1.empty()){
                stk2.push(stk1.top());
                stk1.pop();
            }
            return stk2.top();
        } 
    }

    /** Returns whether the queue is empty. */
    bool empty() {
        return stk1.empty() && stk2.empty();
    }
};

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.peek();
 * bool param_4 = obj.empty();
 */
```



