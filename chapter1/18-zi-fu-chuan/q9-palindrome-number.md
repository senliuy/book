# 9. Palindrome Number

直达：https://leetcode.com/problems/palindrome-number/description/

Determine whether an integer is a palindrome. Do this without extra space.

## 分析

首先取得整数的长度len。

使用x%10取低位，x/pow\(10, len-1\)取高位，循环判断直到x到个位。

## 代码

### C++

```cpp
class Solution {
public:
    bool isPalindrome(int x) {
        if (x < 0) return false;
        if (x < 10) return true;
        int temp_x = x;
        int x_len = 0;
        while(temp_x != 0){
            x_len++;
            temp_x /= 10;
        }
        while(x_len > 1 && x%10 == int(x/pow(10, x_len-1))){
            x -= int(x/pow(10,x_len-1)) * pow(10,x_len-1);
            x /= 10;
            x_len -= 2;
        }
        if (x_len < 2) return true;
        else return false;
    }
};
```



