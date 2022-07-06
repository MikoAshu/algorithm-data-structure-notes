# LeetCode 63 - Unique Paths II



You are given an `m x n` integer array `grid`. There is a robot initially located at the **top-left corner** (i.e., `grid[0][0]`). The robot tries to move to the **bottom-right corner** (i.e., `grid[m-1][n-1]`). The robot can only move either down or right at any point in time.

An obstacle and space are marked as `1` or `0` respectively in `grid`. A path that the robot takes cannot include **any** square that is an obstacle.

Return _the number of possible unique paths that the robot can take to reach the bottom-right corner_.

The testcases are generated so that the answer will be less than or equal to `2 * 109`.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/04/robot1.jpg)

```
Input: obstacleGrid = [[0,0,0],[0,1,0],[0,0,0]]
Output: 2
Explanation: There is one obstacle in the middle of the 3x3 grid above.
There are two ways to reach the bottom-right corner:
1. Right -> Right -> Down -> Down
2. Down -> Down -> Right -> Right
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/11/04/robot2.jpg)

```
Input: obstacleGrid = [[0,1],[0,0]]
Output: 1
```

&#x20;

**Constraints:**

* `m == obstacleGrid.length`
* `n == obstacleGrid[i].length`
* `1 <= m, n <= 100`
* `obstacleGrid[i][j]` is `0` or `1`.

## Solution

```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        HashMap<String, Integer> memo = new HashMap<>();
        return uniqueM(obstacleGrid, obstacleGrid.length, obstacleGrid[0].length, memo);
    }
    
     public int uniqueM(int[][] obstacleGrid,
                        int r,
                        int c,
                        HashMap<String, Integer> memo) {
         // check the zeros ffirst as we will need that not to have index out of bounds values
         if(r == 0 || c == 0) return 0;
         // check if the value at that index is occupied or not and block all paths that pass througg it
         if(obstacleGrid[r - 1][c - 1] == 1) return 0;
         // check the memo
         if(memo.containsKey(r + "," + c)) return memo.get(r + "," + c);
         // base case that returns a true value
         if(r == 1 && c == 1) return 1;

         // put the key inside the memo
         memo.put(r + "," + c, uniqueM(obstacleGrid, r-1, c, memo) + uniqueM(obstacleGrid, r, c -1, memo));
         return memo.get(r + "," + c);
     }
}
```
