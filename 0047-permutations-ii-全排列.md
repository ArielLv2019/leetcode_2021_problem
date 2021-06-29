[Question] (https://leetcode.com/problems/permutations-ii/)

```
Given a collection of numbers, nums, that might contain duplicates, return all possible unique permutations in any order.

Example 1:
Input: nums = [1,1,2]
Output:
[[1,1,2],
 [1,2,1],
 [2,1,1]]
 
Example 2:
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
 
Constraints:
1 <= nums.length <= 8
-10 <= nums[i] <= 10
```
```cpp
class Solution {
public:
    vector<vector<int>> permuteUnique(vector<int>& nums) {
        used = vector<bool>(nums.size(), false);
        // 先对nums排序，保证相同的数字都相邻
        sort(nums.begin(), nums.end());
        
        //从0开始，
        //依次考虑[0,..., n-1]这n个位置放哪个数
        permuteUnique(nums, 0);
        return result;
    }
    
private:
    void permuteUnique(vector<int>& nums, int idx) {
        // 说明已经填完n个位置，将per存入结果，结束递归
        if(per.size() == nums.size()){
            result.emplace_back(per); // make a copy for other language
            return;
        }
        
        // 考虑第idx个位置填入哪个数
        // "从还没有用过的数"中选一个放在当前位置idx
        for(int i = 0; i < nums.size(); i++){
            if(used[i] || 
               // 解决重复问题，保证在填第idx个数的时候，重复数字只会被填入一次。
               // 保证每次填入的数字一定是在这个数所在重复数集合中“从左往右第一个未被填过的数字"
               (i > 0 && nums[i] == nums[i-1] && !used[i-1])){ 
                continue;
            }
            
            used[i] = true;
            per.emplace_back(nums[i]);
                
            // 递归查找下一个位置填什么
            permuteUnique(nums, idx+1);
                
            // 还原现场
            used[i] = false;
            per.pop_back();          
        }
    }
    
    vector<vector<int>> result;
    vector<int> per;
    vector<bool> used;
};
```
