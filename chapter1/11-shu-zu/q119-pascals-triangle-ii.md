# 119. Pascal's Triangle II

直达：[https://leetcode.com/problems/pascals-triangle-ii/description/](https://leetcode.com/problems/pascals-triangle-ii/description/)

Given an indexk, return thekthrow of the Pascal's triangle.

For example, given k= 3,  
Return`[1,3,3,1]`.

**Note:**  
Could you optimize your algorithm to use onlyO\(k\) extra space?

## 分析：

类似Q118, 不同之处是可以将中间结果保存在输出向量中。

注：输出向量的第i个元素可以表示为k\(k-1\)...\(k-i\)/1\*2\*...\*i, 但这种方法计算可能发生数组越界现象。

## C++代码

```cpp
class Solution {
public:
    vector<int> getRow(int rowIndex) {
        // if(rowIndex == 0) return vector<int>(1,1);
        vector<int> res(rowIndex+1,0);
        for(int i=0;i<rowIndex+2;i++){
            if(i == 0) res[0] = 1;
            else{
                for(int j = i; j>=0; j--){
                    if(j == i || j == 0) res[j] == 1;
                    else res[j] = res[j]+res[j-1];
                }
            }
        }
        return res;
    }
};
```



