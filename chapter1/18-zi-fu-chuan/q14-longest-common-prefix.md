# 14. Longest Common Prefix

直达：[https://leetcode.com/problems/longest-common-prefix/description/](https://leetcode.com/problems/longest-common-prefix/description/)

Write a function to find the longest common prefix string amongst an array of strings.

## 分析

没有什么难度的一道题，两层循环对比公共前缀即可。

## C++代码

```cpp
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        if (strs.size() == 0) return "";
        if (strs.size() == 1) return strs[0];
        string res="";
        for(int j = 0; j<INT_MAX; j++){
            for(int i = 1; i < strs.size(); i++){
                if(strs[0].size() <= j || strs[i].size() <= j || strs[i][j] != strs[0][j])    return res;
            }
            res += strs[0][j];
        }
        return res;
    }
};
```



