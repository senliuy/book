# 84. Largest Rectangle in Histogram

## 问题

直达：[https://leetcode.com/problems/largest-rectangle-in-histogram/description/](https://leetcode.com/problems/largest-rectangle-in-histogram/description/)

Given n non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.

![](https://leetcode.com/static/images/problemset/histogram.png)

Above is a histogram where width of each bar is 1, given height =`[2,1,5,6,2,3]`.

![](https://leetcode.com/static/images/problemset/histogram_area.png)  


The largest rectangle is shown in the shaded area, which has area =`10`unit.

For example,  
Given heights =`[2,1,5,6,2,3]`,  
return`10`.

## 分析：

1. 计算以每个bar为高的最大矩形区域面积，返回最大值；
2. 如果bar的高度逐渐增高，则围城的面积逐渐增大，不需要计算；
3. 如果bar的高度开始递减（设为k），则要计算递减之前的最大面积，为了避免重复计算，从右向左计算至小于height\[k\]的时候停止计算即可；
4. 可在数组后面添加一个高度为0的bar，用于辅助清空临时堆栈；
5. 从左向右遍历，再从右向左计算面积，明显用堆栈存储效率更高，由于可以通过下标访问到高度，存储下标即可。

## 举例：

1. 索引i=0, height\[0\] = 2，堆栈为空，直接将2的下标0压栈，i++；
2. i=1，height\[1\]=1 &lt; 2, 开始从右向左计算面积；

   1. i=0的bar的面积是0的长度1乘以高度2，即为2，保存res=2；

   2. 堆栈为空，停止弹出。

3. i=1, 堆栈为空，将i=1压栈, i++；

4. i=2, height\[i\]=5&gt;height\[stk.top\(\)\]=1, 将i=2压栈，i++;

5. i=3, height\[i\]=6&gt;height\[stk.top\(\)\]=5. 将i=3压栈，i++, 此时，stk=\[1,2,3\];

6. i=4, 此时height\[i\]=2&lt;height\[stk.top\(\)\], 开始从右向左计算面积；

   1. 弹出栈顶h=stk.top\(\)=3, stk.pop\(\), 此时的矩形区域的长是\(i-stk.top\(\)-1\), 高是height\[h\], area = \(i-stk.top\(\)-1\)\*height\[h\] = 6, res更新为6;

   2. 弹出栈顶h=stk.top\(\)=2, area = \(i-stk.top\(\)-1\) \* height\[h\] = \(4-1-1\)\*5 = 10.

7. i=4, stk.top\(\)=1 &lt; height\[i\]=2, 4入栈，i++;

8. i=5, 5入栈，i++, 此时stk=\[1,4,5\];

i=6, 遍历到添加的0高度，开始从右向左计算面积，并清空堆栈；

1. h=stk.top\(\)=5, stk.pop\(\), area = \(6-stk.top\(\)-1\) \* height\[5\] = 3, stk = \[1,4\], res = 10;

2. h=stk.top\(\)=4, stk.pop\(\), area = \(6-stk.top\(\)-1\) \* height\[4\] = 8, stk = \[1\], res = 10;

3. h=stk.top\(\)=1, stk.pop\(\), 堆栈为空，area = \(i\)\*height\[h\] = 6, res = 10;

4. 由此可以返回最大值10

## C++实现：

```cpp
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        stack<int> stk;
        heights.push_back(0);
        int res = 0;
        for (int i = 0; i < heights.size(); i++){
            if(stk.empty() || heights[i] > heights[stk.top()]){
                stk.push(i);
            }else{
                int h = stk.top();
                stk.pop();
                res = max(res, (stk.empty()?i:i-stk.top()-1) * heights[h]);
                i--;
            }
        }
        return res;
    }
};
```



