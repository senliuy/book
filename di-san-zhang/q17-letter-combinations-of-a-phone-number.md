# 17. Letter Combinations of a Phone Number

Given a digit string, return all possible letter combinations that the number could represent.

A mapping of digit to letters \(just like on the telephone buttons\) is given below.

![](http://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png)

```
Input:Digit string "23"
Output:["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```

**Note:**  
Although the above answer is in lexicographical order, your answer could be in any order you want.

## 分析

递归求解。

## C++代码

```cpp
class Solution {
public:
    void letterCombinations_helper(vector<string>&res, string digits, int idx, string path){
        vector<string> phone = {"abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
        string str = phone[digits[idx]-'2'];
        for(int i=0; i<str.size(); i++){
            if(idx == digits.size() -1){
                res.push_back(path+str[i]);
            }else{
                letterCombinations_helper(res, digits, idx+1, path+str[i]);
            }
        }
    }
    vector<string> letterCombinations(string digits) {
        vector<string> res;
        int idx = 0;
        string path = "";
        letterCombinations_helper(res, digits, idx, path);
        return res;
    }
};
```



