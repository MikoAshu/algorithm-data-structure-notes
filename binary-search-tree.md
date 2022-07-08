# Binary Search

**Notes**

* Mid point is calculated as `left + (right - left)/2`
* // Easy implementation - return the mid value if it matches first

```java
class Solution {
    public int search(int[] nums, int target) {
        int mid, l = 0, r=nums.length-1;
        while(l<=r) {
            mid = l + (r - l)/2;
            if(nums[mid] == target) return mid;
            if(nums[mid] < target) l = mid + 1;
            else r = mid - 1;
        }
        return -1;
    }
}
```

*
