# 169. Majority Element

直达：[https://leetcode.com/problems/majority-element/description/](https://leetcode.com/problems/majority-element/description/)

Given an array of sizen, find the majority element. The majority element is the element that appears**more than**`⌊ n/2 ⌋`times.

You may assume that the array is non-empty and the majority element always exist in the array.

## 分析

本题很容易想到基于排序或者哈希表的方法，但是排序的方法的时间复杂度是O\(nlogn\)，而哈希表需要占用额外的存储空间，若要使用O\(n\)且不占用额外存储空间的方法，可以使用Boyer-Moore投票方法

Boyer-Moore投票方法是每次删除两个不同的数，直到最后剩下的一定是出现次数大于$$\lfloor n/2 \rfloor$$的数，但是数组的删除是非常困难的，因为每删除一个元素都要移动数组，所以可以采用计数器的方式。

设当前统计的数是flag，遇到等于flag的数count+1，否则count - 1，如果count &lt; 0， 则表示该数不一定是要返回的数，则可以换一个数。

## C++代码

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int major = nums[0];
        int count = 1;
        for(int i = 1; i<nums.size(); i++){
            if(count == 0){
                major = nums[i];
                count =1;
            }else if(major == nums[i]) count++;
            else count--;
        }
        return major;
    }
};
```



