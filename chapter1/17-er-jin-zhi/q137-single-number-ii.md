# 137. Single Number II

直达：[https://leetcode.com/problems/single-number-ii/description/](https://leetcode.com/problems/single-number-ii/description/)

Given an array of integers, every element appearsthreetimes except for one, which appears exactly once. Find that single one.

**Note:**  
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

## 分析

和Q136类似，对于一个数组，出现3次的数字取和摩3之后结果是0，依次遍历，按位相加后摩3，得到的结果便是只出现一次的那个数。例如数组\[3, 3, 5, 3, 4, 5, 5\] 对应的二进制编码是\[011, 011, 101, 011, 100, 101, 101\], 按位取和之后是\[4, 3, 6\]，摩3之后是\[1, 0, 0\]. 对应的二进制是4，即只出现一次的那个数。

每一位的运算符合下面规则：

00 + 0 -&gt; 00, 01 + 0 -&gt; 01, 10 + 0 -&gt; 10

00 + 1 -&gt; 01, 01 + 1 -&gt; 10, 10 + 1 -&gt; 00

设二进制高位为a, 低位是b，遍历到的数是num，对应的真值表是 

| 输入a | 输入b | num | 输出a | 输出b | a ^ num | b ^ num |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 0 | 1 | 0 | 0 | 1 | 0 | 1 |
| 1 | 0 | 0 | 1 | 0 | 1 | 0 |
| 0 | 0 | 1 | 0 | 1 | 1 | 1 |
| 0 | 1 | 1 | 1 | 0 | 1 | 0 |
| 1 | 0 | 1 | 0 | 0 | 0 | 1 |

输入a, 输入b^num，输出b对应的真值表是

| 输入a | 输入b^num | 输出b |
| :--- | :--- | :--- |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 0 |
| 1 | 1 | 0 |

于是有

输出b = ~输入a & \(输入b^num\)

输出b，输入a^num， 输出a对应的真值表是

| 输出b | 输入a^num | 输出a |
| :--- | :--- | :--- |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 0 |
| 1 | 1 | 0 |

于是有

输出a = ~输出b&\(输入a^num\)

于是遍历的更新规则是

b = ~a&\(b^num\)

a = ~b&\(a^num\)

按照算法来说，得到的结果应该是出现1次的那个数，直接返回b即可。

## C++代码

```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int a = 0;
        int b = 0;
        for (auto num : nums){
            b = (num^b) & ~a;
            a = (num^a) & ~b;
        }
        return b;
    }
};
```



