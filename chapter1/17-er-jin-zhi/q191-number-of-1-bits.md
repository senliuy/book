# 191. Number of 1 Bits

直达：[https://leetcode.com/problems/number-of-1-bits/description/](https://leetcode.com/problems/number-of-1-bits/description/)

Write a function that takes an unsigned integer and returns the number of ’1' bits it has \(also known as the[Hamming weight](http://en.wikipedia.org/wiki/Hamming_weight)\).

For example, the 32-bit integer ’11' has binary representation`00000000000000000000000000001011`, so the function should return 3.

**Credits:**  
Special thanks to[@ts](https://oj.leetcode.com/discuss/user/ts)for adding this problem and creating all test cases.

## 分析：

二进制中，n&\(n-1\)作用是将n的二进制表示中的最低位为1的改为0，每更改一次计数器+1，知道n=0停止。

## C++代码

```cpp
class Solution {
public:
    int hammingWeight(uint32_t n) {
        int res = 0;
        while(n){
            n &= n-1;
            res++;
        }
        return res;
    }
};
```



