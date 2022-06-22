## Leetcode 739 - Daily Temperatures

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