[Question](https://leetcode.com/problems/n-ary-tree-level-order-traversal/)
```
Given an n-ary tree, return the level order traversal of its nodes' values.

Nary-Tree input serialization is represented in their level order traversal, each group of children is separated by the null value (See examples).


Example 1:
Input: root = [1,null,3,2,4,null,5,6]
Output: [[1],[3,2,4],[5,6]]

Example 2:
Input: root = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]
Output: [[1],[2,3,4,5],[6,7,8,9,10],[11,12,13],[14]]
```
### 代码一
+ pair + queue
```cpp
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
    vector<vector<int>> levelOrder(Node* root) {
        // 处理特殊情况，空的树
        if(root == nullptr){
            return {};
        }
        
        vector<vector<int>> result;
        
        // q = {[node, depth],...}
        queue<pair<Node*, int>> q;
        q.emplace(make_pair(root, 0));
        while(!q.empty()){
            // 1. 取出队头
            auto node = q.front().first;
            auto depth = q.front().second;
            q.pop();
            
            // 判断数组不为空，避免数组越界
            if(result.size() <= depth){
                result.emplace_back(vector<int>{});
            }
            // 存入结果
            result[depth].emplace_back(node->val);
            
            // 2. 扩展一层
            for(Node* child : node->children){
                q.emplace(make_pair(child, depth+1));
            }
        }
            
        return result;
    }
};
```

### 代码二
+ queue + 计数
```cpp
class Solution {
public:
    vector<vector<int>> levelOrder(Node* root) {
        // 处理特殊情况，空的树
        if(root == nullptr){
            return {};
        }
        
        vector<vector<int>> result;
        
        // 每次遍历队列的时候先记录当前层的元素个数
        queue<Node*> q;
        q.emplace(root);
        while(!q.empty()){
            // 记录当前层的个数 && 处理当前层
            int len = q.size();
            result.emplace_back(vector<int>{});
            
            for(int i = 0; i < len; i++){
                // 1. 取出队头
                auto node = q.front();
                q.pop();
                
                // 2. 存入结果
                result.back().emplace_back(node->val);
                
                // 3. 扩展一层
                for(Node* child : node->children){
                    q.emplace(child);
                }
            }            
        }
            
        return result;
    }
};
```
