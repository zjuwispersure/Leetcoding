



代码：

```
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int size1 = nums1.size();
        int size2 = nums2.size();
        int size = size1 + size2;
        if(size % 2 == 1){
            int result = findKth(nums1, 0, size1 - 1, nums2, 0, size2 - 1, size/2);
            return result;
        }else {
            int left = findKth(nums1, 0, size1 - 1, nums2, 0, size2 - 1, size/2);
            int right = findKth(nums1, 0, size1 - 1, nums2, 0, size2 - 1, size/2 + 1);
            return (left + right)/2;
        }
    }
    int findKth(vector<int> &a, int astart, int aend, vector<int> &b, int bstart, int bend, int k){
        int alength = aend - astart + 1;
        int blength = bend - bstart + 1;
        if(alength > blength){
            return findKth(b, bstart, bend, a, astart, aend, k);
        }
        if(k == 0){
            return Math.min(a[astart], b[bstart]);
        }
        int k1 = Math.min(k/2, alength);
        int k2 = k -k1;
        if(a[astart + k1 -1] > b[bstart + k2 - 1]){
            findKth(a, astart, aend, b, astart + k2, bend, k1);
        } else if (a[astart + k1 -1] > b[bstart + k2 - 1]){
            findKth(a, astart + k1, aend, b, bstart, bend, k2)
        } else {
            return a[astart];
        }
    }
};
```

