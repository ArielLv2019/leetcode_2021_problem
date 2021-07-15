[Question](https://leetcode-cn.com/problems/find-median-from-data-stream/)

```
中位数是有序列表中间的数。如果列表长度是偶数，中位数则是中间两个数的平均值。

例如，

[2,3,4] 的中位数是 3

[2,3] 的中位数是 (2 + 3) / 2 = 2.5

设计一个支持以下两种操作的数据结构：

void addNum(int num) - 从数据流中添加一个整数到数据结构中。
double findMedian() - 返回目前所有元素的中位数。
示例：

addNum(1)
addNum(2)
findMedian() -> 1.5
addNum(3) 
findMedian() -> 2
进阶:

如果数据流中所有整数都在 0 到 100 范围内，你将如何优化你的算法？
如果数据流中 99% 的整数都在 0 到 100 范围内，你将如何优化你的算法？
```
```
测试用例：
["MedianFinder","addNum","findMedian","addNum","findMedian","addNum","findMedian","addNum","findMedian","addNum","findMedian"]
[[],[-1],[],[-2],[],[-3],[],[-4],[],[-5],[]]
["MedianFinder","addNum","addNum","findMedian","addNum","findMedian"]
[[],[1],[2],[],[3],[]]
```
#### 解题思路
```
用大顶堆和小顶堆实现
1）用大顶堆存left数据的前半部分； 用小顶堆right存数据的后半部分，
始终保证left.size() >= right.size()
2) 插入一个新数据的时候:
    如果 left.empty() or left.top() > num, 插入left；否则插入right
    调整两个堆的大小，以满足left.size() >= right.size()
        当left.size() < right.size(): 移动right---->left
        当right.size()+1 < left.size(): left---->right
3）查找中位数的时候:
    如果left.size()==right.size()(是偶数长度)，返回两个堆顶的均值
    否则，返回left.top()--->始终保证left.size() >= right.size()
```
#### 代码实现
```cpp
class MedianFinder {
public:
    /** initialize your data structure here. */
    MedianFinder() {

    }
    
    void addNum(int num) {
        (left.empty() || left.top() > num)? left.emplace(num) : right.emplace(num);

        // adjust the size of the two heap
        while(left.size() < right.size()){
            left.emplace(right.top());
            right.pop();
        }

        while(right.size() + 1 < left.size()){
            right.emplace(left.top());
            left.pop();
        }     
    }
    
    double findMedian() {
        if(left.size() == right.size()){
            return (double(left.top()) + right.top()) / 2;
        }

        return left.top();
    }
private:
    priority_queue<int, vector<int>, less<int>> left; // max_heap
    priority_queue<int, vector<int>, greater<int>> right; // min_heap
};

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder* obj = new MedianFinder();
 * obj->addNum(num);
 * double param_2 = obj->findMedian();
 */
```
