[Question](https://leetcode.com/problems/permutations/)
```
Given an array nums of distinct integers, return all the possible permutations. You can return the answer in any order.

Example 1:
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

Example 2:
Input: nums = [0,1]
Output: [[0,1],[1,0]]

Example 3:
Input: nums = [1]
Output: [[1]]
```
```cpp
// cpp: recursive(递归）
class Solution {
public:
    vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int>> result;
        permute(nums, result, 0);
        return result;
    }
private:
    void permute(vector<int>& nums, vector<vector<int>>& result, int begin){
        if(begin >= nums.size()){
            result.emplace_back(nums);
            return;
        }
        
        for(int i = begin; i < nums.size(); i++){
            swap(nums[i], nums[begin]);
            permute(nums, result, begin+1);
            swap(nums[i], nums[begin]); //reset
        }
        
        return ;
    }
};
```
