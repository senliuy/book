# 91. Decode Ways

直达：[https://leetcode.com/problems/decode-ways/description/](https://leetcode.com/problems/decode-ways/description/)

A message containing letters from`A-Z`is being encoded to numbers using the following mapping:

```
'A' -> 1
'B' -> 2
...
'Z' -> 26
```

Given an encoded message containing digits, determine the total number of ways to decode it.

For example,  
Given encoded message`"12"`, it could be decoded as`"AB"`\(1 2\) or`"L"`\(12\).

The number of ways decoding`"12"`is 2.

## 分析：

当遍历到字符串 s 的第k个位置时，对应的路径的数量取决于第k-1和k-2个位置的内容和路径数。所以要采用动态规划求解，具体要分成下面几种情况：

1. `s[i] == 0`
   1. 如果`0<(s[i-1]-'0')*10+s[i]-'0'<=26`, 则第k个位置的路径数等于第k-2个位置的路径数, 例如`*10*`，要从左侧`*`处断开；
   2. 反之，路径数为0，例如`*30*`.无法继续，路径数为0，直接返回0。
2. `s[i] != 0`

   1. 如果`s[i-1]==0`

      1. 如果`0<(s[i-1]-'0')*10+s[i]-'0'<=26`，则第k个位置的路径数等于第k-1个位置的路径数；

      2. 否则，路径数为0，直接返回，如`*00*`这种情况

   2. 如果`s[i-1] != 0`

      1. 如果`0<(s[i-1]-'0')*10+s[i]-'0'<=26`，则第k个位置的路径数等于第k-1个位置的路径数加上k-2个位置的路径数，如`*123*`，i指向3，断成`*12,3*`或者`*1,23*`都可以；
      2. 否则，则第k个位置的路径数等于第k-1个位置的路径数，如`*128*`只能断成`*12,8*`。

## C++代码：

```cpp
class Solution {
public:
    int numDecodings(string s) {
        int n = s.size();
        if(n == 0) return 0;
        if(s[0] == '0') return 0;
        vector<int> dp(n+1, 0);
        dp[0] = 1;
        dp[1] = 1;
        for(int i = 1; i < n; i++){
            int temp = ((s[i-1]-'0')*10+s[i]-'0');
            if(s[i] == '0'){
                if (0 < temp && 26 >= temp) dp[i+1] = dp[i-1];
                else return 0;
            }else{
                if(s[i-1] != '0'){
                    if (0 < temp && 26 >= temp) dp[i+1] = dp[i] + dp[i-1];
                    else dp[i+1] = dp[i];
                }else{
                    if (0 < temp && 26 >= temp) dp[i+1] = dp[i];
                    else return 0;
                }
            }
        }
        return dp[n];
    }
};
```



