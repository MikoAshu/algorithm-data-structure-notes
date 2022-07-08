# LeetCode 844 - Backspace String Compare

Given two strings `s` and `t`, return `true` _if they are equal when both are typed into empty text editors_. `'#'` means a backspace character.

Note that after backspacing an empty text, the text will continue empty.

&#x20;

**Example 1:**

```
Input: s = "ab#c", t = "ad#c"
Output: true
Explanation: Both s and t become "ac".
```

**Example 2:**

```
Input: s = "ab##", t = "c#d#"
Output: true
Explanation: Both s and t become "".
```

**Example 3:**

```
Input: s = "a#c", t = "b"
Output: false
Explanation: s becomes "c" while t becomes "b".
```

&#x20;

**Constraints:**

* `1 <= s.length, t.length <= 200`
* `s` and `t` only contain lowercase letters and `'#'` characters.

&#x20;

**Follow up:** Can you solve it in `O(n)` time and `O(1)` space?

## Solution

### Stack based solution

```java
class Solution {
    public boolean backspaceCompare(String s, String t) {
        // create two stacks
        Stack<Character> stk1 = new Stack<>();
        Stack<Character> stk2 = new Stack<>();
        
        // add each element to the stack and pop elements if the stack is not empty and value is'#'
        // otherwise add elements to the stack
        for(int i = 0; i < s.length(); i++){
            if(s.charAt(i) == '#') {
                if(!stk1.isEmpty()) stk1.pop();
            } else {
                stk1.push(s.charAt(i));
            }
        }
        
        for(int i=0; i< t.length(); i++){
             if(t.charAt(i) == '#') {
                if(!stk2.isEmpty()) stk2.pop();
            } else {
                stk2.push(t.charAt(i));
            }  
        }
        
        // is stack size doesnt match, return false
        if(stk1.size() != stk2.size()) return false;
        
        // pop each element from the stack and compare the values
        while(!stk1.isEmpty() && !stk2.isEmpty()){
            if(stk1.pop() != stk2.pop()) return false;
        }
        return true;
    }
}
```

* Time Complexity: O(M + N)O(M+N), where M, NM,N are the lengths of `S` and `T` respectively.
* Space Complexity: O(M + N)O(M+N).

### **Two Pointer**

**Intuition**

When writing a character, it may or may not be part of the final string depending on how many backspace keystrokes occur in the future.

If instead**,** we iterate through the string in reverse, then we will know how many backspace characters we have seen, and therefore whether the result includes our character.

**Algorithm**

Iterate through the string in reverse. If we see a backspace character, the next non-backspace character is skipped. If a character isn't skipped, it is part of the final answer.

```java
class Solution {
    public boolean backspaceCompare(String S, String T) {
        int i = S.length() - 1, j = T.length() - 1;
        int skipS = 0, skipT = 0;

        while (i >= 0 || j >= 0) { // While there may be chars in build(S) or build (T)
            while (i >= 0) { // Find position of next possible char in build(S)
                if (S.charAt(i) == '#') {skipS++; i--;}
                else if (skipS > 0) {skipS--; i--;}
                else break;
            }
            while (j >= 0) { // Find position of next possible char in build(T)
                if (T.charAt(j) == '#') {skipT++; j--;}
                else if (skipT > 0) {skipT--; j--;}
                else break;
            }
            // If two actual characters are different
            if (i >= 0 && j >= 0 && S.charAt(i) != T.charAt(j))
                return false;
            // If expecting to compare char vs nothing
            if ((i >= 0) != (j >= 0))
                return false;
            i--; j--;
        }
        return true;
    }
}
```
