# 198. House Robber

直达：https://leetcode.com/problems/house-robber/description/

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and**it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight**without alerting the police**.

**Credits:**  
Special thanks to[@ifanchu](https://oj.leetcode.com/discuss/user/ifanchu)for adding this problem and creating all test cases. Also thanks to[@ts](https://oj.leetcode.com/discuss/user/ts)for adding additional test cases.

## 分析

动态规划的经典题目，动态规则也非常简单。第i天盗得的总和是第i-2天，或者第i-3天最大值加上nums\[i\]， 所以有动态规划更新规则：

```
dp[i+1] = max(dp[i-1], dp[i-2]) + nums[i];
```

注：为了编码方便，动态规划数组添加了一个0的头。

## C++代码

```
class Solution {
public:
    int rob(vector<int>& nums) {
        int len = nums.size();
        if(len == 0) return 0;
        vector<int> dp(len+1, 0);
        dp[1] = nums[0];
        for (int i = 1; i < len; i++){
            if (i == 1) dp[i+1] = dp[0] + nums[i];
            else dp[i+1] = max(dp[i-1], dp[i-2]) + nums[i];
        }
        return max(dp[len], dp[len-1]);
    }
};
```



