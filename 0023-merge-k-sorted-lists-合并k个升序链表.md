[Question](https://leetcode.com/problems/merge-k-sorted-lists/)
```
You are given an array of k linked-lists lists, each linked-list is sorted in ascending order.

Merge all the linked-lists into one sorted linked-list and return it.

Example 1:
Input: lists = [[1,4,5],[1,3,4],[2,6]]
Output: [1,1,2,3,4,4,5,6]
Explanation: The linked-lists are:
[
  1->4->5,
  1->3->4,
  2->6
]
merging them into one sorted list:
1->1->2->3->4->4->5->6

Example 2:
Input: lists = []
Output: []

Example 3:
Input: lists = [[]]
Output: []
```
### 解题思路一
+ 循环
### 代码
```cpp
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        ListNode* result = nullptr;
        for(auto& list : lists){
            result = mergeTwoList(result, list);
        }       
        return result;
    }
```
### 解题思路二
+ 分治
    + 划分[0, n-1]这n个链表的合并问题为两个子问题[0, mid], [mid+1, n-1]; 然后将这两个子问题的结果合并
 
### 代码

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        if(lists.size() == 0){
            return nullptr;
        }

        return merge(lists, 0, lists.size()-1);
    }

private:
    // 分治合并链表集合，递归实现
    ListNode* merge(vector<ListNode*> lists, int l, int r){
        // 终止条件
        if(l == r){ return lists[l]; }
        if(l > r){ return nullptr; }

        // 划分[0, n-1]这n个链表的合并问题为两个子问题[0, mid], [mid+1, n-1]; 然后将这两个子问题的结果合并
        // new1 = merge(lists, l, mid)
        // new2 = merge(lists, mid+1, r)
        // mergeTwoList(new1, new2);
        int mid = l + (r - l) / 2;
        return mergeTwoList(merge(lists, l, mid), merge(lists, mid+1, r));
    }

    // 合并两个单链表
    ListNode* mergeTwoList(ListNode* l1, ListNode* l2){
        if(l1 == nullptr || l2 == nullptr){
            return (l1 == nullptr)? l2 : l1;
        }
        ListNode dummyHead;
        ListNode* pre = &dummyHead;
        while(l1 != nullptr && l2 != nullptr){
            if(l1->val < l2->val){
                pre->next = l1;
                l1 = l1->next;
            }else{
                pre->next = l2;
                l2 = l2->next;
            }
            pre = pre->next;
        }

        pre->next = (l1 == nullptr)? l2 : l1;
        return dummyHead.next;
    }
};
```
