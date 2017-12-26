# 107. Binary Tree Level Order Traversal II

直达：https://leetcode.com/problems/binary-tree-level-order-traversal-ii/description/

Given a binary tree, return thebottom-up level ordertraversal of its nodes' values. \(ie, from left to right, level by level from leaf to root\).

For example:  
Given binary tree`[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

return its bottom-up level order traversal as:

```
[
  [15,7],
  [9,20],
  [3]
]
```

## 分析

和Q102思想一样，只需用堆栈重新将数组重新排序即可。

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
    vector<vector<int>> levelOrderBottom(TreeNode* root) {
        vector<vector<int>> res1;
        vector<vector<int>> res2;
        if(root==NULL) return res1;
        helper(res1, root, 0);
        stack<vector<int>> stk;
        for(int i = 0; i<res1.size(); i++){
            stk.push(res1[i]);
        }
        while(!stk.empty()){
            res2.push_back(stk.top());
            stk.pop();
        }
        return res2;
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



