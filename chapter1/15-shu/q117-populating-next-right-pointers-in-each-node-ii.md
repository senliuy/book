# 117. Populating Next Right Pointers in Each Node II

直达：https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/description/

Follow up for problem "Populating Next Right Pointers in Each Node".

What if the given tree could be any binary tree? Would your previous solution still work?

**Note:**

* You may only use constant extra space.

For example,  
Given the following binary tree,

```
         1
       /  \
      2    3
     / \    \
    4   5    7

```

After calling your function, the tree should look like:

```
         1 -> NULL
       /  \
      2 -> 3 -> NULL
     / \    \
    4-> 5 -> 7 ->NULL
```

## 分析

对于任意一棵树来说，可以分成下面三种情况

1. 若左子树存在，右子树也存在，左子树的next是右子树，右子树的next是父节点的兄弟节点的第一个孩子（root的大侄子）；
2. 若左子树存在，右子树不存在，左子树的next是父节点的兄弟节点的第一个孩子；
3. 若左子树不存在，右子树存在，右子树的next是父节点的兄弟节点的第一个孩子；

所以问题的关键是寻找root的大侄子，依次查看root-&gt;next是否存在左右子树，否则，root = root-&gt;next;

同样，可以通过递归操作完成。

```cpp
/**
 * Definition for binary tree with next pointer.
 * struct TreeLinkNode {
 *  int val;
 *  TreeLinkNode *left, *right, *next;
 *  TreeLinkNode(int x) : val(x), left(NULL), right(NULL), next(NULL) {}
 * };
 */
class Solution {
public:
    void connect(TreeLinkNode *root) {
        if(!root) return;
        TreeLinkNode *temp = root->next;
        while(temp){
            if(temp->left){
                temp = temp->left;
                break;
            }else if(temp->right){
                temp = temp->right;
                break;
            }
            temp = temp->next;
        }
        if(root->right) root->right->next = temp;
        if(root->left) root->left->next = (root->right)?(root->right):(temp);
        connect(root->right);
        connect(root->left);
    }
};
```



