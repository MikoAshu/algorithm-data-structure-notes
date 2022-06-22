# Leetcode 739 - Daily Temperatures

Given an array of integers `temperatures` represents the daily temperatures, return _an array_ `answer` _such that_ `answer[i]` _is the number of days you have to wait after the_ `ith` _day to get a warmer temperature_. If there is no future day for which this is possible, keep `answer[i] == 0` instead.

&#x20;

**Example 1:**

```
Input: temperatures = [73,74,75,71,69,72,76,73]
Output: [1,1,4,2,1,1,0,0]
```

**Example 2:**

```
Input: temperatures = [30,40,50,60]
Output: [1,1,1,0]
```

**Example 3:**

```
Input: temperatures = [30,60,90]
Output: [1,1,0]
```

&#x20;

**Constraints:**

* `1 <= temperatures.length <= 105`
* `30 <= temperatures[i] <= 100`

### Solution

On this question, the simple solution is to create a stack of array to keep track of the value and the index and add them to the stack after removing the lesser elements from the stack and calculating the index between them

to keep track of the next element, we will have an array to store the difference -

```cpp
int[] res = new int[temperatures.length];
```

Then finally return the result array

```cpp
class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        if(temperatures.length == 0) return new int[] {-1, -1};
        Stack<int[]> stack = new Stack<>();
        int[] res = new int[temperatures.length];
        for(int i=0; i < temperatures.length; i++) {
            while(!stack.isEmpty() && stack.peek()[0] < temperatures[i]){
                int[] temp = stack.pop();
                res[temp[1]] = i - temp[1];
            }
            stack.push(new int[]{temperatures[i], i});
        }
        return res;
    }
}
```
