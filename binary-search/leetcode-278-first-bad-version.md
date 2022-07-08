# LeetCode 278 - First Bad Version

<mark style="background-color:green;">Easy</mark>

You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad.

Suppose you have `n` versions `[1, 2, ..., n]` and you want to find out the first bad one, which causes all the following ones to be bad.

You are given an API `bool isBadVersion(version)` which returns whether `version` is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API.

&#x20;

**Example 1:**

```
Input: n = 5, bad = 4
Output: 4
Explanation:
call isBadVersion(3) -> false
call isBadVersion(5) -> true
call isBadVersion(4) -> true
Then 4 is the first bad version.
```

**Example 2:**

```
Input: n = 1, bad = 1
Output: 1
```

&#x20;

**Constraints:**

* `1 <= bad <= n <= 231 - 1`

## Solution

```java
/* The isBadVersion API is defined in the parent class VersionControl.
      boolean isBadVersion(int version); */

public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        if(n<2) return n;
        return vc(0, n);
    }
    
    public int vc(int l, int r){
        // find mid value
        int mid = l + (r - l)/2;
        // if the value is bad and the previous is good, it means it is the first bad so we return
        if(isBadVersion(mid) && !isBadVersion(mid-1)) return mid;
        // otherwise, search left if the value is bad or right is the value is not bad
        if(isBadVersion(mid)) return vc(l,mid-1);
        else return vc(mid+1,r);
    }
}
```
