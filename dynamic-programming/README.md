# Dynamic Programming

## Notes

* When checking base cases - values that return 0 like grid navigation, put them first as they will prevent additional lookups and manupulations you do after that - check  [LeetCode 63 ](leetcode-63-unique-paths-ii.md)where there is an additional check if the path is blocked and there is a check for the values at that position inside the grid. so, having the null values first will prevent index out-of-bounds errors

