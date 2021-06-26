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
