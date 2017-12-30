# 120. Triangle

直达：https://leetcode.com/problems/triangle/description/

Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

For example, given the following triangle  


```
[    
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
```

The minimum path sum from top to bottom is`11`\(i.e.,2+3+5+1= 11\).

**Note:**  
Bonus point if you are able to do this using onlyO\(n\) extra space, wherenis the total number of rows in the triangle.

## 分析

算法思路类似于Q119, 不同之处在于矩阵的更新方法，由求和变成求最小值。

## C++代码

```cpp
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        if(triangle.size() == 0) return 0;
        vector<int> res(triangle.size(), 0);
        for(int i = 0; i<triangle.size(); i++){
            if(i == 0) res[0] = triangle[0][0];
            else{
                for(int j=i;j>=0;j--){
                    if(j == i) res[j] = triangle[i][j] + res[j-1];
                    else if(j == 0) res[j] = triangle[i][j] + res[j];
                    else res[j] = min(res[j], res[j-1]) + triangle[i][j];
                }
            }
        }
        int min_res = res[0];
        for(int k = 0; k<res.size(); k++){
            min_res = min(res[k], min_res);
        }
        return min_res;
    }
};
```



