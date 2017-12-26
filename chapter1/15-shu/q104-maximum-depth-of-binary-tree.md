# 104. Maximum Depth of Binary Tree

直达：https://leetcode.com/problems/maximum-depth-of-binary-tree/description/

Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

## 分析：

深度优先遍历树，保存两个变量，一个是当前节点的深度，另外一个是已经遍历的树节点的最大的深度。返回最大深度即可。

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
    int maxDepth(TreeNode* root) {
        int h = 0;
        int res = 0;
        if(!root) return 0;
        helper(root, h, res);
        return res;
    }
private:
    void helper(TreeNode* root, int h, int& res){
        if(root==NULL) res = max(h, res);
        else{
            helper(root->left, h+1, res);
            helper(root->right, h+1, res);
        }
    }
};
```



