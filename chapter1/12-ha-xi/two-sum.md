# 1. Two Sum

直达：https://leetcode.com/problems/two-sum/description/

Given an array of integers, return**indices**of the two numbers such that they add up to a specific target.

You may assume that each input would have**exactly**one solution, and you may not use thesameelement twice.

**Example:**

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

## 分析

用哈希表存储已经遍历的元素\(hash\[key\]=val\), 如果遇到和满足target的，则将两个数返回，否则返回空

## C++代码

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map <int, int> hash;
        vector<int> res;
        for(int i=0; i<nums.size(); i++){
            if (hash.find(target - nums[i]) != hash.end()){
                res.push_back(hash[target-nums[i]]);
                res.push_back(i);
                return res;
            }else{
                hash[nums[i]] = i;
            }
        }
        return res;
    }
};
```



