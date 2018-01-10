# 171. Excel Sheet Column Number

直达：https://leetcode.com/problems/excel-sheet-column-number/description/

Related to question [Excel Sheet Column Title](https://leetcode.com/problems/excel-sheet-column-title/)

Given a column title as appear in an Excel sheet, return its corresponding column number.

For example:

```
    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
```

**Credits:**  
Special thanks to[@ts](https://leetcode.com/discuss/user/ts)for adding this problem and creating all test cases.

分析

这道题本质上是二十六进制转十进制

C++代码

```cpp
class Solution {
public:
    int titleToNumber(string s) {
        int len = s.size();
        int res = 0;
        for (int i = 0; i < len; i++){
            res += pow(26, i) * (s[len-1-i]-'A'+1);
        }
        return res;
    }
};
```



