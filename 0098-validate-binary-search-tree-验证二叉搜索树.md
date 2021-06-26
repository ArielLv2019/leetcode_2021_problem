[Question](https://leetcode.com/problems/validate-binary-search-tree/)
```
```
```cpp
// cpp 递归
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
    bool isValidBST(TreeNode* root) {        
        return isValidBST(root, nullptr, nullptr);
    }
    
private:
    bool isValidBST(TreeNode* root, TreeNode* minVal, TreeNode* maxVal){
        if( root == nullptr ){
            return true;
        }
        if(minVal != nullptr && root->val <= minVal->val){
            return false;
        }
        if(maxVal != nullptr && root->val >= maxVal->val){
            return false;
        }
        
        return isValidBST(root->left, minVal, root) && isValidBST(root->right, root, maxVal);
    } 
};
```
