# 118. Pascal's Triangle

直达：[https://leetcode.com/problems/pascals-triangle/description/](https://leetcode.com/problems/pascals-triangle/description/)

GivennumRows, generate the firstnumRowsof Pascal's triangle.

For example, givennumRows= 5,  
Return

```
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

## 分析

帕斯卡三角的特征是

从1开始，以下第i行的第j个元素满足：

1. 如果 j==0 \|\| i == j, pas\[i\]\[j\] = 1；
2. 否则 pas\[i\]\[j\] = pas\[i-1\]\[j-1\] + pas\[i\]\[j\]

## C++代码

```cpp
class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> res;
        for(int i = 0; i<numRows; i++){
            if(i == 0) res.push_back(vector<int>(1,1));
            else{
                vector<int> t;
                for(int j = 0; j<=i; j++){
                    if(j == 0 || j == i)    t.push_back(1);
                    else t.push_back(res[i-1][j-1] + res[i-1][j]);
                }
                res.push_back(t);
            }
        }
        return res;
    }
};
```



