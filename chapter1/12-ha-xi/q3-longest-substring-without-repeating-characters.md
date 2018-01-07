# 3. Longest Substring Without Repeating Characters

直达：https://leetcode.com/problems/longest-substring-without-repeating-characters/description/

Given a string, find the length of the **longest substring **without repeating characters.

**Examples:**

Given`"abcabcbb"`, the answer is`"abc"`, which the length is 3.

Given`"bbbbb"`, the answer is`"b"`, with the length of 1.

Given`"pwwkew"`, the answer is`"wke"`, with the length of 3. Note that the answer must be a**substring**,`"pwke"`is asubsequenceand not a substring.

## 分析



## C++代码

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        unordered_map <char, int> hash;
        int res = 0;
        int cur_res = 0;
        for (int i = 0; i<s.size(); i++){
            if (hash.find(s[i]) == hash.end())  cur_res += 1;
            else    cur_res = min((i-hash[s[i]]), (cur_res+1));
            hash[s[i]] = i;
            res = res>cur_res?res:cur_res;
        }
        return res;
    }
};
```



