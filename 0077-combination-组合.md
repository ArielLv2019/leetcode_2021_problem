[Question](https://leetcode.com/problems/combinations/)
```
Given two integers n and k, return all possible combinations of k numbers out of the range [1, n].

You may return the answer in any order.


Example 1:
Input: n = 4, k = 2
Output:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]

Example 2:
Input: n = 1, k = 1
Output: [[1]]
```
[Answer](https://leetcode.wang/leetCode-77-Combinations.html)

### Topic:
+ Array, Backtracing

### 解题思路一
+ 递归枚举1，2，3，。。。，n这n个数选或不选，
+ 终止条件1: 当idx>n（或idx == n+1) 时终止

+ 优化终止条件2:
++	选的数已经超过k个
++	或者，把剩下的数全选也不够k个
++	就可以退出

### 代码
```cpp
class Solution {
public:
    vector<vector<int>> combine(int n, int k) {      
        combine(n, k, 1);
        return res;
    }
    
    void combine(int n, int k, int idx){
        // // 递归终止条件1
        // if(idx > n){ // 或者if(idx == n+1){
        //    // 当有k个数时才将元素放入结果
        //    if(comb.size() == k){
        //         //如果是其他语言，需要make a copy
        //         // 例如java： res.add(new ArrayList<Integer>(comb));
        //         res.emplace_back(comb);             
        //    } 
        //    return ;
        // }
        
        // 优化递归终止条件：如果选的数个数已经超过k， 或者把剩下的数全选也不够k个， 就直接退出
        if(comb.size() > k || comb.size() + n - idx + 1 < k){
            return;
        }
        
        if(idx == n+1){
            res.emplace_back(comb);
            return ;
        }
          
        // 不选
        combine(n, k, idx+1);
        
       // 选
        comb.emplace_back(idx);
        combine(n, k, idx+1);
        comb.pop_back();     //还原现场
    }
private:
    vector<vector<int>> res;
    vector<int> comb;
};
```
```cpp
//cpp: Backtracing
class Solution {
public:
    vector<vector<int>> combine(int n, int k) {
        vector<vector<int>> res;
        vector<int> comb;
        combine(res, comb, 1, n, k);
        return res;
    }
    
    void combine(vector<vector<int>>& res, vector<int>& comb, int start, int n, int k){
        if(k == 0){
            res.emplace_back(comb);
            return ;
        }
        
        for(int i = start; i <= n; i++){
            comb.emplace_back(i);
            combine( res, comb, i+1, n, k-1);
            comb.pop_back();
        }
        
        return ;
    }
};
```
