# 89. Gray Code

# 问题：

直达：[https://leetcode.com/problems/gray-code/description/](https://leetcode.com/problems/gray-code/description/)

The gray code is a binary numeral system where two successive values differ in only one bit.

Given a non-negative integernrepresenting the total number of bits in the code, print the sequence of gray code. A gray code sequence must begin with 0.

For example, givenn= 2, return`[0,1,3,2]`. Its gray code sequence is:

```
00 - 0
01 - 1
11 - 3
10 - 2
```

**Note:**  
For a givenn, a gray code sequence is not uniquely defined.

For example,`[0,2,3,1]`is also a valid gray code sequence according to the above definition.

For now, the judge is able to judge based on one instance of gray code sequence. Sorry about that.

# 分析：

当n=1时，输出初始化为`[0,1]`,n=2时，交替的向尾部添加`[0,1], [1,0]` \(奇数位置填`[0,1]`, 偶数位置填`[1,0]`\). 结果即是`[00, 10, 11, 01]`。尾部加0就是乘2，尾部加一就是乘2再加1.

以此类推, 第k个在第k-1个的数组的每个数的基础上在尾部分别交替添加`[0,1], [1,0]`。

因此，迭代的进行更新数组即可。

# 算法：

```cpp
class Solution {
public:
    vector<int> grayCode(int n) {
        vector<int> res;
        res.push_back(0);
        if(n == 0) return res;
        res.push_back(1);
        for(int i=1; i<n; i++){
            res = helper(res, i);
        }
        return res;
    }
private:
    vector<int> helper(vector<int>& nums, int k){
        vector<int> res;
        int add_num = pow(2, k);
        for(int i=0; i<nums.size(); i++){
            if(i%2 == 0){
                res.push_back(nums[i]*2);
                res.push_back(nums[i]*2+1);
            }else{
                res.push_back(nums[i]*2+1);
                res.push_back(nums[i]*2);
            }
        }
        return res;
    }
};
```



