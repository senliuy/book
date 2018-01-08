# 155. Min Stack

直达：https://leetcode.com/problems/min-stack/description/

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

* push\(x\) -- Push element x onto stack.
* pop\(\) -- Removes the element on top of the stack.
* top\(\) -- Get the top element.
* getMin\(\) -- Retrieve the minimum element in the stack.

**Example:**

```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.
```

## 分析

栈的压入和弹出过程可能会导致堆栈最小值发生变化，因此需要一个结构来保存当前堆栈的最小值。

1. 例如数组$$[3, 2, 4, 5, ..., a_n] $$（其中省略号的数都大于2），此时无虑在最小值1后面的数是怎样变化的，getMin\(\)返回的最小值都是2。
2. 但是如果省略号中存在一个1，例如\[3, 2, 4, 5, ..., 1, ..., a\_n\], 此时第二个省略号无论怎么变化，返回的都是1，第一个省略号内的内容无论怎么变化，返回的都是2.
3. 同理，如果第二个省略号中含有更小的值，情况将类似2。

所以，根据分析：

1. 根据3，数据结构应该采用堆栈保存最小值
2. 根据2，如果出栈的值等于最小值，则要更新最小堆栈，即弹出栈顶元素。
3. 根据1，如果入栈的值小于等于当前最小值，则最小堆栈压入该元素。
   1. 为什么要有等于呢？考虑下面情况，例如依次将数组\[3, 2, 4, 5, 7, 2\]入栈，如果没有等于的话，最小栈中保存的元素应该是\[3, 2\], 堆栈的元素是\[3,2,4,5,7,2\], 堆栈弹出一个元素，由于弹出的元素等于getMin\(\), 根据2，最小栈也要弹出栈顶，此时最小栈为\[3\], 显然是不正确的。

C++代码

```cpp
class MinStack {
private:
    stack<int> stk;
    stack<int> min_stk;
public:
    /** initialize your data structure here. */
    // MinStack() {}
    void push(int x) {
        stk.push(x);
        if(min_stk.empty() || x <= min_stk.top()) min_stk.push(x);
    }
    void pop() {
        if(stk.top() == min_stk.top()) min_stk.pop();
        stk.pop();
    }
    int top() {
        return stk.top();
    }
    int getMin() {
        return min_stk.top();
    }
};
```



