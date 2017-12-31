# 129. Sum Root to Leaf Numbers

直达：[https://leetcode.com/problems/sum-root-to-leaf-numbers/description/](https://leetcode.com/problems/sum-root-to-leaf-numbers/description/)

Given a binary tree containing digits from`0-9`only, each root-to-leaf path could represent a number.

An example is the root-to-leaf path`1->2->3`which represents the number`123`.

Find the total sum of all root-to-leaf numbers.

For example,

```
    1
   / \
  2   3
```

The root-to-leaf path`1->2`represents the number`12`.  
The root-to-leaf path`1->3`represents the number`13`.

Return the sum = 12 + 13 =`25`.

## 分析

类似于[Q112,](https://senliuy.gitbooks.io/leetcode/content/chapter1/15-shu/q112-path-sum.html) 不同之处在于去路径之和的时候要对之前的路径乘以10。

## C++代码

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int sumNumbers(TreeNode* root) {
        int res = 0;
        if(!root) return 0;
        helper(root, root->val, res, 0);
        return res;
    }
private:
    void helper(TreeNode* root, int path, int& res, int height){
        if (!root->left && !root->right){
            res += path;
            return;
        }else{
            if(root->left) helper(root->left, 10 * path + root->left->val, res, height+1);
            if(root->right) helper(root->right, 10 * path + root->right->val, res, height+1);
        }
    }
};
```



