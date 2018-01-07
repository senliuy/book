# 6. ZigZag Conversion

直达：[https://leetcode.com/problems/zigzag-conversion/description/](https://leetcode.com/problems/zigzag-conversion/description/)

The string`"PAYPALISHIRING"`is written in a zigzag pattern on a given number of rows like this: \(you may want to display this pattern in a fixed font for better legibility\)

```
P   A   H   N
A P L S I I G
Y   I   R
```

And then read line by line:`"PAHNAPLSIIGYIR"`

Write the code that will take a string and make this conversion given a number of rows:

```
string convert(string text, int nRows);
```

`convert("PAYPALISHIRING", 3)`should return`"PAHNAPLSIIGYIR"`

## 分析

这道题更像是一道数学题，关键是找到返回字符串的字符位置和原字符串的字符位置的对应关系。0-n的整数数组（字符串下标）更容易看到规律，例如numRows = 5

对应Z形是

```
0       8           16
1     7 9        15 17
2   6   10    14    18    ...
3 5     11 13       19 21
4       12          20
```

两个竖的间距是2\*\(numRows-1\)，在第i行\(i&gt;=1 && i&lt;=numRows-2 \)，中间要插入一个间距为2\*\(numRows-i\)的数字。

换成字符串时，注意下标不要超过字符串的长度。

## C++代码

```cpp
class Solution {
public:
    string convert(string s, int numRows) {
        if(s.size() < 3) return s;
        if(numRows <= 1) return s;
        string res;
        for (int i = 0; i <= numRows-1; i++){
            int j = i;
            while(j < s.size()){
                res+=(s[j]);
                if(j + 2*(numRows-1-i) < s.length() && i > 0 && i < numRows - 1){
                    res+=(s[j + 2*(numRows-1-i)]);
                }
                j += 2 * (numRows-1);
            }
        }
        return res;   
    }
};
```



