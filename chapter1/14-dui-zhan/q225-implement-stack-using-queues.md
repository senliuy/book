# Q255. Implement Stack using Queues

Implement the following operations of a stack using queues.

* push\(x\) -- Push element x onto stack.
* pop\(\) -- Removes the element on top of the stack.
* top\(\) -- Get the top element.
* empty\(\) -- Return whether the stack is empty.

**Notes:**

* You must use only standard operations of a queue -- which means only`push to back`,`peek/pop from front`,`size`, and`is empty`operations are valid.
* Depending on your language, queue may not be supported natively. You may simulate a queue by using a list or deque \(double-ended queue\), as long as you use only standard operations of a queue.
* You may assume that all operations are valid \(for example, no pop or top operations will be called on an empty stack\).

## 分析

用一个队列实现即可，stack和queue的区别在于弹出的顺序不同。所以在每次插入时，通过循环的方式将新的元素移动到最后的位置即可。

## C++代码

```cpp
class MyStack {
public:
    /** Initialize your data structure here. */
    queue<int> que1;
    MyStack() {
        
    }
    
    /** Push element x onto stack. */
    void push(int x) {
        que1.push(x);
        for(int i=0; i< que1.size()-1; i++){
            que1.push(que1.front());
            que1.pop();
        }
    }
    
    /** Removes the element on top of the stack and returns that element. */
    int pop() {
        int res = que1.front();
        que1.pop();
        return res;
    }
    
    /** Get the top element. */
    int top() {
        return que1.front();
    }
    
    /** Returns whether the stack is empty. */
    bool empty() {
        return que1.empty();
    }
};

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack obj = new MyStack();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.top();
 * bool param_4 = obj.empty();
 */
```



