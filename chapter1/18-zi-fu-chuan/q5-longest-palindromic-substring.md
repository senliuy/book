# 5. Longest Palindromic Substring

直达：https://leetcode.com/problems/longest-palindromic-substring/description/

Given a string**s**, find the longest palindromic substring in**s**. You may assume that the maximum length of**s**is 1000.

**Example:**

```
Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```

**Example:**

```
Input: "cbbd"
Output: "bb"
```

## 分析

遍历字符串，从遍历到的字符开始向两边查找，判断是否满足回文。注意需要区分奇数子串和偶数子串两种情况。

## C++代码

```cpp
class Solution {
public:
    string longestPalindrome(string s) {
        int res_left = 0;
        int res_right = 0;
        if (s.size() < 2)  return s;
        for(int i=0; i<=s.size()-1;i++){
            // 奇数长度子串
            int left = i-1;
            int right = i+1;
            while(s[left] == s[right] && left >= 0 && right <= s.size()-1){
                left--; right++;
            }
            if((right-left-2) > (res_right-res_left)){
                res_right = right-1;
                res_left = left+1;
            }
            // 偶数长度子串
            right = i+1;
            left = i;
            while(s[left] == s[right] && left >= 0 && right <= s.size()-1){
                left--; right++;
            }
            if((right-left-2) > (res_right-res_left)){
                res_right = right-1;
                res_left = left+1;
            }
        }
        return s.substr(res_left, (res_right-res_left+1));
    }
};
```



