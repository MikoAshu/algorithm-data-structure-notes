# Dynamic Programming

## Notes

* When checking base cases - values that return 0 like grid navigation, put them first as they will prevent additional lookups and manupulations you do after that - check  [LeetCode 63 ](leetcode-63-unique-paths-ii.md)where there is an additional check if the path is blocked and there is a check for the values at that position inside the grid. so, having the null values first will prevent index out-of-bounds errors
* _**\*\*\*\* If you find yourself choosing between one or more options and asking you to decide between choices, dynamic programming is the right approach - check leetcode 97 - interleaving string**_
* _**If you are provided with two values and multiple choices, a dynamic programming grid or grid based solutions might be your best bet check leetcode 97 - interleaving string**_

