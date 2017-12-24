# 90. Subsets II

直达: [https://leetcode.com/problems/subsets-ii/description/](https://leetcode.com/problems/subsets-ii/description/)

Given a collection of integers that might contain duplicates,**nums**, return all possible subsets \(the power set\).

**Note:**The solution set must not contain duplicate subsets.

For example,  
If **nums**=`[1,2,2]`, a solution is:

```
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```

## 分析:

是[Q78](https://senliuy.gitbooks.io/leetcode/di-san-zhang/q78-subsets.html)的扩展，不同之处在于输入的是含有重复元素的数组。

处理方法是在插入元素的时候，略过和它前面内容相同的元素。

## C++代码

```cpp
class Solution {
public:
    vector<vector<int>> subsetsWithDup(vector<int>& nums) {
        vector<vector<int>> res;
        vector<int> path;
        sort(nums.begin(), nums.end());
        helper(res, path, nums, 0, 0);
        return res;
    }
private:
    void helper(vector<vector<int>>& res, vector<int>& path, vector<int> nums, int pos, int cnt){
        if(cnt <= nums.size()){
            res.push_back(path);
            for(int i = pos; i<nums.size(); i++){
                if(i!=pos && nums[i] == nums[i-1]) continue;
                path.push_back(nums[i]);
                helper(res, path, nums, i+1, cnt+1);
                path.pop_back();
            }
        }
    }
};
```



