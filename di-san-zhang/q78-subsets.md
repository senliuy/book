# 7.8 Subsets

直达: [https://leetcode.com/problems/subsets/description/](https://leetcode.com/problems/subsets/description/)

Given a set of**distinct**integers,nums, return all possible subsets \(the power set\).

**Note:**The solution set must not contain duplicate subsets.

For example,  
If **nums **=`[1,2,3]`, a solution is:

```
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

## 分析

求子集是递归的典型题目之一，每次向路径中添加一个数即可。

## C++代码

```cpp
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> res;
        vector<int> path;
        helper(res, path, nums, 0, 0);
        return res;
    }
private:
    void helper(vector<vector<int>>& res, vector<int>& path, vector<int> nums, int pos, int cnt){
        if(cnt <= nums.size()){
            res.push_back(path);
        }
        for(int i = pos; i<nums.size(); i++){
            path.push_back(nums[i]);
            helper(res, path, nums, i, cnt+1);
            path.pop_back();
        }
    }
};
```



