[题目介绍](https://leetcode.com/problems/find-median-from-data-stream/)



Median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value. So the median is the mean of the two middle value.

For example,

```
[2,3,4]`, the median is `3
[2,3]`, the median is `(2 + 3) / 2 = 2.5
```

Design a data structure that supports the following two operations:

- void addNum(int num) - Add a integer number from the data stream to the data structure.
- double findMedian() - Return the median of all elements so far.

 

**Example:**

```
addNum(1)
addNum(2)
findMedian() -> 1.5
addNum(3) 
findMedian() -> 2
```

 

**Follow up:**

1. If all integer numbers from the stream are between 0 and 100, how would you optimize it?
2. If 99% of all integer numbers from the stream are between 0 and 100, how would you optimize it?



## 解法：sort



```C++
class MedianFinder {
public:
    /** initialize your data structure here. */
    vector<double> store;
    MedianFinder() {
        
    }
    
    void addNum(int num) {
        store.push_back(num);
    }
    
    double findMedian() {
        sort(store.begin(), store.end());
        int n = store.size();
        return (n%2==1?store[n/2]:(store[n/2-1] + store[n/2])*0.5);
    }
};

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder* obj = new MedianFinder();
 * obj->addNum(num);
 * double param_2 = obj->findMedian();
 */
```



插入排序，lower_bound函数和insert函数

> 功能：函数lower_bound()在first和last中的前闭后开区间进行二分查找，返回**大于或等于val的第一个元素位置**。如果所有元素都小于val，则返回last的位置.
>
> 注意：如果所有元素都小于val，则返回last的位置，且last的位置是**越界**的！！

>iterator insert( iterator loc, const TYPE &val );
>
>在指定位置loc前插入值为val的元素,返回指向这个元素的迭代器

```
class MedianFinder {
    vector<int> store; // resize-able container

public:
    // Adds a number into the data structure.
    void addNum(int num)
    {
        if (store.empty())
            store.push_back(num);
        else
            store.insert(lower_bound(store.begin(), store.end(), num), num);     // binary search and insertion combined
    }

    // Returns the median of current data stream
    double findMedian()
    {
        int n = store.size();
        return n & 1 ? store[n / 2] : (store[n / 2 - 1] + store[n / 2]) * 0.5;
    }
};
```



