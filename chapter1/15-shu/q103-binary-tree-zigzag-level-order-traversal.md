# 93. Binary Tree Zigzag Level Order Traversal

直达：https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/description/

Given a binary tree, return thezigzag level ordertraversal of its nodes' values. \(ie, from left to right, then right to left for the next level and alternate between\).

For example:  
Given binary tree`[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

return its zigzag level order traversal as:

```
[
  [3],
  [20,9],
  [15,7]
]
```

## 分析

Q102层次遍历的变形，用堆栈重新排列Q102结果的行数摩2等于1的那一行元素。

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
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        vector<vector<int>> res;
        if(root==NULL) return res;
        helper(res, root, 0);
        for(int i=0; i<res.size(); i++){
            if(i%2 == 1){
                stack<int> stk;
                for(int j=0; j<res[i].size();j++){
                    stk.push(res[i][j]);
                }
                int k = 0;
                while(!stk.empty()){
                    res[i][k] = stk.top();
                    k++;
                    stk.pop();
                }
            }
        }
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



