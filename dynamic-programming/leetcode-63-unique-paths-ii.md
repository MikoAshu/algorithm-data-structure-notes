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

### Solution

**Algorithm**

1. If the first cell i.e. `obstacleGrid[0,0]` contains `1`, this means there is an obstacle in the first cell. Hence the robot won't be able to make any move and we would return the number of ways as `0`.
2. Otherwise, if `obstacleGrid[0,0]` has a `0` originally we set it to `1` and move ahead.
3. Iterate the first row. If a cell originally contains a `1`, this means the current cell has an obstacle and shouldn't contribute to any path. Hence, set the value of that cell to `0`. Otherwise, set it to the value of previous cell i.e. `obstacleGrid[i,j] = obstacleGrid[i,j-1]`
4. Iterate the first column. If a cell originally contains a `1`, this means the current cell has an obstacle and shouldn't contribute to any path. Hence, set the value of that cell to `0`. Otherwise, set it to the value of previous cell i.e. `obstacleGrid[i,j] = obstacleGrid[i-1,j]`
5.  Now, iterate through the array starting from cell `obstacleGrid[1,1]`. If a cell originally doesn't contain any obstacle then the number of ways of reaching that cell would be the sum of number of ways of reaching the cell above it and number of ways of reaching the cell to the left of it.

    ```
     obstacleGrid[i,j] = obstacleGrid[i-1,j] + obstacleGrid[i,j-1]
    ```
6. If a cell contains an obstacle set it to `0` and continue. This is done to make sure it doesn't contribute to any other path.

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

OR

```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {

        int R = obstacleGrid.length;
        int C = obstacleGrid[0].length;

        // If the starting cell has an obstacle, then simply return as there would be
        // no paths to the destination.
        if (obstacleGrid[0][0] == 1) {
            return 0;
        }

        // Number of ways of reaching the starting cell = 1.
        obstacleGrid[0][0] = 1;

        // Filling the values for the first column
        for (int i = 1; i < R; i++) {
            obstacleGrid[i][0] = (obstacleGrid[i][0] == 0 && obstacleGrid[i - 1][0] == 1) ? 1 : 0;
        }

        // Filling the values for the first row
        for (int i = 1; i < C; i++) {
            obstacleGrid[0][i] = (obstacleGrid[0][i] == 0 && obstacleGrid[0][i - 1] == 1) ? 1 : 0;
        }

        // Starting from cell(1,1) fill up the values
        // No. of ways of reaching cell[i][j] = cell[i - 1][j] + cell[i][j - 1]
        // i.e. From above and left.
        for (int i = 1; i < R; i++) {
            for (int j = 1; j < C; j++) {
                if (obstacleGrid[i][j] == 0) {
                    obstacleGrid[i][j] = obstacleGrid[i - 1][j] + obstacleGrid[i][j - 1];
                } else {
                    obstacleGrid[i][j] = 0;
                }
            }
        }

        // Return value stored in rightmost bottommost cell. That is the destination.
        return obstacleGrid[R - 1][C - 1];
    }
```



* Time Complexity: O(M \times N)O(M×N). The rectangular grid given to us is of size M \times NM×N and we process each cell just once.
* Space Complexity: O(1)O(1). We are utilizing the `obstacleGrid` as the DP array. Hence, no extra space.
