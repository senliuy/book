# 84. Largest Rectangle in Histogram

## 问题

直达：[https://leetcode.com/problems/largest-rectangle-in-histogram/description/](https://leetcode.com/problems/largest-rectangle-in-histogram/description/)

该题目是求柱状图的bar围成的最大矩形的面积，如下图height =`[2,1,5,6,2,3]`的面积是10.

![](/assets/import.png)

分析：

1. 如果bar的高度逐渐增高，则围城的面积逐渐增大，不需要计算；
2. 如果bar的高度开始递减（设为k），则要计算递减之前的最大面积，为了避免重复计算，从右向左计算至小于height\[k\]的时候停止计算即可；
3. 可在数组后面添加一个高度为0的bar，用于辅助清空临时堆栈；
4. 从左向右遍历，再从左向右计算面积，明显用堆栈存储效率更高，由于可以通过下标访问到高度，存储下标即可。

举例：

1. 索引i=0, height\[0\] = 2，堆栈为空，直接将2的下标0压栈，i++；
2. i=1，height\[1\]=1 &lt; 2, 开始从右向左计算面积；

   1. i=0的bar的面积是0的长度1乘以高度2，即为2；

   2. 堆栈为空，停止弹出。

3. i=1, 堆栈为空，将i=1压栈；
4. 


