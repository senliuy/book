# 16. 3Sum Closet

直达：[https://leetcode.com/problems/3sum-closest/description/](https://leetcode.com/problems/3sum-closest/description/)

Given an arraySofnintegers, find three integers inSsuch that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

```
    For example, given array S = {-1 2 1 -4}, and target = 1.

    The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```

## 分析

问题的核心是两个指针的操作。循环遍历数组，将遍历到的元素取做中心点，从该点的两侧出发初始化left，和right两个指针，如果三个位置只和小于target，则右指针向右移动一位，否则左指针向左移动一位，每次移动如果找到更接近的三组数，则更新返回结果。重复上面过程直到不能移动为止。

## C++代码

```cpp
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        sort(nums.begin(), nums.end());
        int res = nums[0] + nums[1] + nums[2];
        for(int cen = 0; cen < nums.size(); cen++){
            int left = cen - 1;
            int right = cen + 1;
            int sum = nums[left] + nums[cen] + nums[right];
            while( (left >= 0) && (right <= nums.size()-1)){
                sum = nums[left] + nums[cen] + nums[right];
                if(sum > target){
                    if(abs(target-sum)<abs(res-target)) res = sum;
                    if(left > 0)    left--;
                    else    break;
                }
                else if(sum < target){
                    if(abs(target-sum)<abs(res-target)) res = sum;
                    if (right < nums.size()-1)   right++;
                    else    break;
                }
                else return target;
            }
        }
        return res;
    }
};
```



