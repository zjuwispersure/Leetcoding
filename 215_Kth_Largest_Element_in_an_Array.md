[题目介绍](https://leetcode.com/problems/kth-largest-element-in-an-array/)

Find the **k**th largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

**Example 1:**

```
Input: [3,2,1,5,6,4] and k = 2
Output: 5
```

**Example 2:**

```
Input: [3,2,3,1,2,4,5,5,6] and k = 4
Output: 4
```

**Note:**
You may assume k is always valid, 1 ≤ k ≤ array's length.



### 解法:排序

先排序然后获取第k个。

```
class Solution {
public:
    static bool cmp(const int a,const int b) {
        return a>b;
    }
    
    int findKthLargest(vector<int>& nums, int k) {
        sort(nums.begin(), nums.end(), cmp);
        return nums[k-1];
    }
};
```



### 解法：nth_element

STL中的nth_element()方法的使用 通过调用nth_element(start, start+n, end) 方法可以使第n大元素处于第n位置（从0开始,其位置是下标为 n的元素），并且比这个元素小的元素都排在这个元素之前，比这个元素大的元素都排在这个元素之后，但不能保证他们是有序的。

 ```
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        nth_element(nums.begin(), nums.begin() + k - 1, nums.end(), greater<int>());
        return nums[k - 1];
    }
};
 ```





### 解法：partial_sort

实现partial_sort的思想是：对原始容器内区间为[first, middle)的元素运行make_heap()操作构造一个最大堆。然后拿[middle, last)中的每一个元素和first进行比較，first内的元素为堆内的最大值。假设小于该最大值，则互换元素位置，并对[first, middle)内的元素进行调整。使其保持最大堆序。

比較完之后在对[first, middle)内的元素做一次对排序sort_heap()操作。使其按增序排列。注意。堆序和增序是不同的。

```
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        partial_sort(nums.begin(), nums.begin() + k, nums.end(), greater<int>());
        return nums[k - 1];
    }
};
```



### 解法：堆排序



```
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        buildMaxHeap(nums);
        for (int i = 0; i < k - 1; i++) {
            swap(nums[0], nums[--heapSize]);
            maxHeapify(nums, 0);
        }
        return nums[0];
    }
private:
    int heapSize;
    
    int left(int i) {
        return (i << 1) + 1;
    }
    
    int right(int i) {
        return (i << 1) + 2;
    }
    
    void maxHeapify(vector<int>& nums, int i) {
        int largest = i, l = left(i), r = right(i);
        if (l < heapSize && nums[l] > nums[largest]) {
            largest = l;
        }
        if (r < heapSize && nums[r] > nums[largest]) {
            largest = r;
        }
        if (largest != i) {
            swap(nums[i], nums[largest]);
            maxHeapify(nums, largest);
        }
    }
    
    void buildMaxHeap(vector<int>& nums) {
        heapSize = nums.size();
        for (int i = (heapSize >> 1) - 1; i >= 0; i--) {
            maxHeapify(nums, i);
        }
    }
};
```

