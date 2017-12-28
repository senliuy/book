# 113. Path Sum II

直达：https://leetcode.com/problems/path-sum-ii/description/

Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

For example:

Given the below binary tree and

`sum = 22`,

```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
```

return

```
[
   [5,4,11,2],
   [5,8,4,5]
]
```

分析

类似于Q112, 只需要保存一个变量path记录当前遍历到的节点，迭代的遍历到叶节点之后如果满足路径之和等于sum后将路径插入返回结果中即可。

C++代码

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
    vector<vector<int>> pathSum(TreeNode* root, int sum) {
        vector<vector<int>> res;
        if(!root) return res;
        vector<int> path;
        treePath(root, sum, res, path);
        return res;
    }
private:
    void treePath(TreeNode* root, int sum, vector<vector<int>>& res, vector<int> path){
        if(!root) return;
        path.push_back(root->val);
        if(!root->left && !root->right && sum == root->val){
            res.push_back(path);
            return;
        }
        treePath(root->left, sum-root->val, res, path);
        treePath(root->right, sum-root->val, res, path);
    }
};
```



