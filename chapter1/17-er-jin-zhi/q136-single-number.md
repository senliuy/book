# 136. Single Number

直达：[https://leetcode.com/problems/single-number/description/](https://leetcode.com/problems/single-number/description/)

Given an array of integers, every element appearstwiceexcept for one. Find that single one.

**Note:**  
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

## 分析

在数组中查找只出现一次的数字，其它数字出现两次。遍历数组，一次将遍历到的数执行亦或，相同的数字通过两次亦或结果是0，遍历之后剩下的那个数就是只出现一次的那个数。

例如数组\[4, 4, 1, 3, 3\] 对应的二进制依次是\[100, 100, 001, 011, 011\], 按位依次亦或得到的结果是\[0, 0, 1\], 即对应只出现一次的1的二进制。ß

## C++代码

```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int res = 0;
        for(int i = 0; i<nums.size(); i++){
            res ^= nums[i];
        }
        return res;
    }
};
```



