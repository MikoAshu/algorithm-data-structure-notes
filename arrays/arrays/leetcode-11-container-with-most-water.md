# LeetCode 11 - Container with most water



You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the `ith` line are `(i, 0)` and `(i, height[i])`.

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return _the maximum amount of water a container can store_.

**Notice** that you may not slant the container.

&#x20;

**Example 1:**

![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question\_11.jpg)

```
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.
```

**Example 2:**

```
Input: height = [1,1]
Output: 1
```

&#x20;

**Constraints:**

* `n == height.length`
* `2 <= n <= 105`
* `0 <= height[i] <= 104`

### Solution

The easy solution is to have a double for loop that checks every combination and compares and updates the max value.

A better solution would be to have two pointers and start them from the opposite end of the array and compares if the value is larger than the already existing one



**Efficient Solution:** &#x20;

* **Approach:** Given an array of heights of lines of boundaries of the container, find the maximum water that can be stored in a container. So start with the first and last element and check the amount of water that can be contained and store that container. Now the question arises is there any better boundaries or lines that can contain maximum water. So there is a clever way to find that. Initially, there are two indices the first and last index pointing to the first and the last element (which acts as boundaries of the container), if the value of first index is less than the value of last index increase the first index else decrease the last index. As the decrease in width is constant, by following the above process the optimal answer can be reached.\
  _The GIF below explains the approach_

![](https://media.geeksforgeeks.org/wp-content/uploads/20200408181228/ezgif.com-gif-maker3.gif)

*   **Algorithm:**&#x20;

    1. Keep two index, _first = 0_ and _last = n-1_ and a value max\_area that stores the maximum area.
    2. Run a loop until first is less than the last.
    3. Update the max\_area with maximum of max\_area and _min(array\[first] , array\[last])\*(last-first)_
    4. if the value at array\[first] is greater the array\[last] then update last as last – 1 else update first as first + 1
    5. Print the maximum area.

    From [https://www.geeksforgeeks.org/container-with-most-water/](https://www.geeksforgeeks.org/container-with-most-water/)
