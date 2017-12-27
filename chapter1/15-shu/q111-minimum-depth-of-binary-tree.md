111. Minimum Depth of Binary Tree

直达：https://leetcode.com/problems/minimum-depth-of-binary-tree/description/

Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

## 分析

使用中间变量保存所有遍历的叶节点的最小深度，递归的遍历即可。

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
    int minDepth(TreeNode* root) {
        int res = INT_MAX;
        if(!root) return 0;
        treeHeight(root, 1, res);
        return res;
    }
private:
    void treeHeight(TreeNode* root, int height, int& minHeight){
        if(!root->left && !root->right){
            minHeight = min(height, minHeight);
            return;
        }
        if(root->left) treeHeight(root->left, height+1, minHeight);
        if(root->right) treeHeight(root->right, height+1, minHeight);
    }
};
```



