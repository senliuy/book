# 167. Two Sum II - Input array is sorted

直达：https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/

Given an array of integers that is already**sorted in ascending order**, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers \(both index1 and index2\) are not zero-based.

You may assume that each input would haveexactlyone solution and you may not use thesameelement twice.

**Input:**numbers={2, 7, 11, 15}, target=9  
**Output:**index1=1, index2=2

## 分析

使用两个指针，一个从左向右查找，一个从右向左查找，不同于O\(n\)方法的每次移动一个值。可以采用二分查找更新到最近的那个值。这样复杂度便是O\(logn\).

## C++代码

```cpp
class Solution {
private:
    int binarySearch(vector<int> nums, int target, int left, int right){
        int mid = (right-left)/2 + left;
        while(left < right){
            if(nums[mid] == target) return mid;
            else if(nums[mid] < target) left = mid+1;
            else right = mid-1;
            mid = (right-left)/2 + left; 
        }
        return mid;
    }
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        int left = 0;
        int right = numbers.size()-1;
        vector<int> res;
        while(left <= right){
            if (numbers[left] + numbers[right] == target){
                res.push_back(left+1);
                res.push_back(right+1);
                return res;
            }else if(numbers[left] + numbers[right] < target){
                left = binarySearch(numbers, target-numbers[right], left+1, right-1);
            }else{
                right = binarySearch(numbers, target-numbers[left], left+1, right-1);
            }
        }
    }
};
```



