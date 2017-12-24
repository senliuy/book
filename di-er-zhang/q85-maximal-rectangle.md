# 85. Maximal Rectangle

## 问题

直达: https://leetcode.com/problems/maximal-rectangle/description/

给出一个含有1和0的二位矩阵，返回右1组成的最大矩形区域的面积

## 解析

该问题是由 Q84 \([https://senliuy.gitbooks.io/leetcode/content/chapter1/14-dui-zhan/largest-rectangle-in-histogram.html](https://senliuy.gitbooks.io/leetcode/content/chapter1/14-dui-zhan/largest-rectangle-in-histogram.html)\) 衍生而来，将问题还原为Q84的方法是将矩阵的每一行都看成一个Q84的问题，其中bar的高度是从matrix\[i\]\[j\]开始，从下往上数不间断的1的个数。显然可以通过动态规划构建。

例如

```
1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0
```

对应的矩阵是

```
1 0 1 0 0
2 0 2 1 1
3 1 3 2 2
4 0 0 3 0
```

C++实现

```cpp
class Solution {
public:
    int maximalRectangle(vector<vector<char>>& matrix) {
        int row = matrix.size();
        if(row == 0) return 0;
        int col = matrix[0].size();
        int res = 0;
        vector<vector<int>> dp(row, vector<int>(col, 0));
        for(int i = 0; i < row; i++){
            for(int j = 0; j < col; j++){
                if(i > 0) dp[i][j] = (matrix[i][j]-'0') * (dp[i-1][j] + (matrix[i][j]-'0'));
                else dp[i][j] = matrix[i][j]-'0';
            }
        }
        
        for(int i = 0; i < row; i++){
            res = max(res, largestRectangleArea(dp[i]));
        }
        return res;
    }
private:
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



