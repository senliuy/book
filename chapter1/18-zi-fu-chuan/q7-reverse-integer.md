# 7. Reverse Integer

直达：[https://leetcode.com/problems/reverse-integer/description/](https://leetcode.com/problems/reverse-integer/description/)

iven a 32-bit signed integer, reverse digits of an integer.

**Example 1:**

```
Input: 123
Output: 321
```

**Example 2:**

```
Input: -123
Output: -321
```

**Example 3:**

```
Input: 120
Output: 21
```

**Note:**  
Assume we are dealing with an environment which could only hold integers within the 32-bit signed integer range. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

## 分析

保存正负号后使用绝对值进行运算。

使用 %10取个位，使用 /10进行右移1位。

使用长整型保存结果（Python不用）以便进行溢出判断。

### 代码

#### C++

```cpp
class Solution {
public:
    int reverse(int x) {
        if (x == INT_MIN) return 0;
        int sign = x>0?1:-1;
        x = sign * x;
        double res = 0;
        while(x != 0){
            res *= 10;
            res += x%10;
            x /= 10;
        }
        if ( (sign > 0 && res > INT_MAX) || (sign < 0 && res-1 > INT_MAX) ) return 0;
        else return sign * int(res);
    }
};
```

#### python

```py
class Solution(object):
    def reverse(self, x):
        """
        :type x: int
        :rtype: int
        """
        pos_x = abs(x)
        res = 0
        while(pos_x > 0):
            res *= 10
            res += pos_x%10
            pos_x = pos_x/10
        if(x < 0):
            res = -res
        if abs(res) > 0x7FFFFFFF:
            return 0
        else:
            return res
```



