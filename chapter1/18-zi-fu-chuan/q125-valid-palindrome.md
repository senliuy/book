# 125. Valid Palindrome

直达：https://leetcode.com/problems/valid-palindrome/description/

Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

For example,  
`"A man, a plan, a canal: Panama"`is a palindrome.  
`"race a car"`isnota palindrome.

**Note:**  
Have you consider that the string might be empty? This is a good question to ask during an interview.

For the purpose of this problem, we define empty string as valid palindrom

## 分析

首先将字符串清洗一下，包括两个步骤：

1. 保留字母和数字
2. 将大写字母转小写

然后使用头尾两个指针判断字符串是否是回文。

## C++代码

```cpp
class Solution {
public:
    bool isPalindrome(string s) {
        string str;
        for(int i = 0; i< s.size(); i++){
            if( (s[i]>='a' && s[i]<='z') || (s[i]>='0' && s[i]<='9')) str+=s[i];
            if(s[i]>='A' && s[i]<='Z') str+= 'a'+(s[i]-'A');
        }
        for(int i=0, j = str.size()-1; i<=j;i++,j--){
            if(str[i]!=str[j]) return false;
        }
        return true;
    }
};
```



