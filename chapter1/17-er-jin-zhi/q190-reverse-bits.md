## 191. Reverse Bits

直达：https://leetcode.com/problems/reverse-bits/description/

Reverse bits of a given 32 bits unsigned integer.

For example, given input 43261596 \(represented in binary as**00000010100101000001111010011100**\), return 964176192 \(represented in binary as**00111001011110000010100101000000**\).

**Follow up**:  
If this function is called many times, how would you optimize it?

Related problem:[Reverse Integer](https://leetcode.com/problems/reverse-integer/)

## 分析

n&1 可以取n的最低位，取完之后右移一位，并将取得的数添加到res的右侧（即右移1位之后再加1）

## C++代码

```cpp
class Solution {
public:
    uint32_t reverseBits(uint32_t n) {
        uint32_t res = 0;
        for(int i = 0; i < 32; i++){
            uint32_t bit = n & 1;
            n = n >> 1;
            res = res << 1;
            res += bit;
        }
        return res;
    }
};
```



