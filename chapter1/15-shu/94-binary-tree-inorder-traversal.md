# 94. Binary Tree Inorder Traversal

直达：[https://leetcode.com/problems/binary-tree-inorder-traversal/description/](https://leetcode.com/problems/binary-tree-inorder-traversal/description/)

Given a binary tree, return theinordertraversal of its nodes' values.

For example:  
Given binary tree`[1,null,2,3]`,

```
   1
    \
     2
    /
   3
```

return`[1,3,2]`.

**Note:**Recursive solution is trivial, could you do it iteratively?

## 分析

树的中序遍历是先遍历左子树，输出根节点后再遍历右节点，迭代的进行即可。

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
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> res;
        if(root) helper(res, root);
        return res;
    }
private:
    void helper(vector<int>& res, TreeNode* root){
        if(root->left) helper(res, root->left);
        res.push_back(root->val);
        if(root->right) helper(res, root->right);
    }
};
```



