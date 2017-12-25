# 102. Binary Tree Level Order Traversal

直达：https://leetcode.com/problems/binary-tree-level-order-traversal/description/

Given a binary tree, return thelevel ordertraversal of its nodes' values. \(ie, from left to right, level by level\).

For example:  
Given binary tree`[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

return its level order traversal as:

```
[
  [3],
  [9,20],
  [15,7]
]
```

## 分析

添加一个变量，用于保存当前遍历的层数，根据层数在输出矩阵中将遍历到的节点值添加进去。

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
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> res;
        if(root==NULL) return res;
        helper(res, root, 0);
        return res;
    }
private:
    void helper(vector<vector<int>>& res, TreeNode* root, int pos){
        if(res.size() <= pos){
            res.push_back(vector<int>(0,0));
        }
        res[pos].push_back(root->val);
        if(root->left) helper(res, root->left, pos+1);
        if(root->right) helper(res, root->right, pos+1);
    }
};
```



