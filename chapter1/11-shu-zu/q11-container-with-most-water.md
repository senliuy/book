# 11. Container With Most Water

直达：[https://leetcode.com/problems/container-with-most-water/description/](https://leetcode.com/problems/container-with-most-water/description/)

Givennnon-negative integers $$a_1, a_2, ..., a_n$$where each represents a point at coordinate $$(i, a_i)$$. $$n$$ vertical lines are drawn such that the two endpoints of lineiis at $$(i, a_i)$$ and $$(i, 0)$$. Find two lines, which together with x-axis forms a container, such that the container contains the most water.

Note: You may not slant the container and $$n$$ is at least 2.

## 分析

从数组两端开始遍历，每次更改高度最小的那个下标。

## C++代码

```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        if (height.size() < 2) return 0;
        int max_area = 0;
        int left = 0;
        int right = height.size() - 1;
        while(left < right){
            int area = 0;
            if (height[left] < height[right]){
                area = (right - left) * height[left];
                left++;
            }else{
                area = (right - left) * height[right];
                right --;
            }
            max_area = max_area > area ? max_area:area;
        }
        return max_area;
    }
};
```



