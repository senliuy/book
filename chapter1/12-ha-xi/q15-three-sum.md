# 15. Three Sum

直达：https://leetcode.com/problems/3sum/description/

Given an arraySofnintegers, are there elementsa,b,cinSsuch thata+b+c= 0? Find all unique triplets in the array which gives the sum of zero.

**Note:**The solution set must not contain duplicate triplets.

```
For example, given array S = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

## 分析

可以将该问题转化成[Q1](https://senliuy.gitbooks.io/leetcode/content/chapter1/12-ha-xi/two-sum.html)，依次将数组的元素作为-target。也可以排序后确定两个值，然后使用二分查找需要的那个值。下面只实现第二个方法。

## C++代码

```cpp
class Solution {
public:
    bool binary_search(vector<int>& nums, int target, int left, int right){
        int mid = 0;
        while(left <= right){
            mid = left + (right - left) /2;
            if(nums[mid] < target) left = mid+1; 
            else if (nums[mid] > target) right = mid-1;
            else return true;
        }
        if (nums[mid] == target) return true;
        else return false;
    }
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> res;
        if (nums.size() <= 2) return res;
        sort(nums.begin(), nums.end());
        for(int i = 0; i <= nums.size() - 3; i++){
            for(int j = i+1; j <= nums.size() - 2; j++){
                if(binary_search(nums, -(nums[i] + nums[j]), j+1, nums.size()-1)){
                    res.push_back({nums[i], nums[j], -(nums[i]+nums[j])});
                }
                while(nums[j+1] == nums[j]) j++;
            }
            while(nums[i+1] == nums[i]) i++;
        }
        return res;
    }
};
```



