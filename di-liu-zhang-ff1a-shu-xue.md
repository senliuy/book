# 168. Excel Sheet Column Title

直达：https://leetcode.com/problems/excel-sheet-column-title/description/

Given a positive integer, return its corresponding column title as appear in an Excel sheet.

For example:

```
    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB 
```

## 分析

这道题是十进制转26进制，但是注意十进制是从1开始计数，所以开始的时候n要减一。

## C++代码

```cpp
class Solution {
public:
    string convertToTitle(int n) {
        string res;
        char temp;
        while(n){
            n -= 1;
            int bit = n%26;
            temp = bit + 'A';
            res = temp + res;
            n /= 26;
        }
        return res;
    }
};
```



