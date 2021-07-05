[Question](https://leetcode.com/problems/n-ary-tree-preorder-traversal/)
```
Given the root of an n-ary tree, return the preorder traversal of its nodes' values.

Nary-Tree input serialization is represented in their level order traversal. Each group of children is separated by the null value (See examples)

 Example 1:
Input: root = [1,null,3,2,4,null,5,6]
Output: [1,3,5,6,2,4]

Example 2:
Input: root = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]
Output: [1,2,3,6,7,11,14,4,8,12,5,9,13,10]
```
### 代码---递归
```cpp
// 递归
/*
// Definition for a Node.
class Node {
public:
    int val;
    vector<Node*> children;

    Node() {}

    Node(int _val) {
        val = _val;
    }

    Node(int _val, vector<Node*> _children) {
        val = _val;
        children = _children;
    }
};
*/

class Solution {
public:
    vector<int> preorder(Node* root) {
        find(root);
        return seq;
    }

private:
    void find(Node* root){
        if(root == nullptr){
            return ;
        }
        
        seq.push_back(root->val);
        for(Node* child : root->children){
            find(child);
        }
    }

    vector<int> seq;
    
};
```
### 代码---迭代
```cpp
// 迭代
// 用一个stack实现
// 根处理完之后，根的孩子节点要从左到右依次处理，所以在入栈的时候，根的孩子要从右到左依次入栈
class Solution {
public:
    vector<int> preorder(Node* root) {
        if(root == nullptr){
            return {};
        }
        vector<int> result;
        stack<Node*> sta;
        sta.emplace(root);
        while(!sta.empty()){
            auto node = sta.top();
            sta.pop();
            result.emplace_back(node->val);
            // 孩子节点从右到左入栈
            for(int i = node->children.size()-1; i >= 0; i --){
                sta.emplace(node->children[i]);
            }
        }
        return result;
    }
};
```
