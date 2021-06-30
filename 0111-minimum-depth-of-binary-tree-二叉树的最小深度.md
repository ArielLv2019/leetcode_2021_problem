[Question](https://leetcode.com/problems/minimum-depth-of-binary-tree/)
```
Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

Note: A leaf is a node with no children.

Example 1:
Input: root = [3,9,20,null,null,15,7]
Output: 2

Example 2:
Input: root = [2,null,3,null,4,null,5,null,6]
Output: 5

```
### 解题思路
+ 自底向上

### 代码

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    int minDepth(TreeNode* root) {
        if(root == nullptr){
            return 0;
        }
        //递归求左右子树的最小深度
        int left = minDepth(root->left);
        int right = minDepth(root->right);
        
        // 如果左右子树有一个为空，最小深度==非空子树的深度+1
        // 如果左右子树都不为空，返回min(left, right)+1
        return (left == 0 || right == 0) ? (left+right+1) : min(left, right)+1;
    }
};
```
