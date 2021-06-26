```
```

## Answer
[Discussion Link](https://leetcode.com/problems/subsets/discuss/27278/C%2B%2B-RecursiveIterativeBit-Manipulation)

```cpp
// cpp: 递归
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> subs;
        vector<int> sub;
        subsets(nums, subs, sub, 0);
        return subs;
    }
    
private:
    void subsets(vector<int>& nums, vector<vector<int>>& subs, vector<int>& sub, int i) {
        subs.emplace_back(sub);
        for(int j = i; j < nums.size(); j++){
            sub.emplace_back(nums[j]);
            subsets(nums, subs, sub, j+1);
            sub.pop_back();
        }
        
        return ;
    }
};
```
