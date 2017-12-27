# 112. Path Sum

直达：[https://leetcode.com/problems/path-sum/description/](https://leetcode.com/problems/path-sum/description/)

Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

For example:

Given the below binary tree and

`sum = 22`

```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \      \
        7    2      1
```

return true, as there exist a root-to-leaf path`5->4->11->2`which sum is 22.

## 分析

保存全局变量path计算根节点到该节点的路径长度，递归的计算即可。另外，用全局变量保存叶节点的路径长度是否是sum。

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
    bool hasPathSum(TreeNode* root, int sum) {
        if(!root) return false;
        bool res = false;
        treePath(root, root->val, sum, res);
        return res;
    }
private:
    void treePath(TreeNode* root, int path, int sum, bool& res){
        if(!root->left && !root->right){
            res = res || (path == sum);
            return;
        }
        if(root->left) treePath(root->left, path+root->left->val, sum, res);
        if(root->right) treePath(root->right, path+root->right->val, sum, res);
    }
};
```



