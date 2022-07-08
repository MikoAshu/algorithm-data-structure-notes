# LeetCode 394. -Decode String

<mark style="background-color:orange;">**Medium**</mark>

Given an encoded string, return its decoded string.

The encoding rule is: `k[encoded_string]`, where the `encoded_string` inside the square brackets is being repeated exactly `k` times. Note that `k` is guaranteed to be a positive integer.

You may assume that the input string is always valid; there are no extra white spaces, square brackets are well-formed, etc. Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, `k`. For example, there will not be input like `3a` or `2[4]`.

The test cases are generated so that the length of the output will never exceed `105`.

&#x20;

**Example 1:**

```
Input: s = "3[a]2[bc]"
Output: "aaabcbc"
```

**Example 2:**

```
Input: s = "3[a2[c]]"
Output: "accaccacc"
```

**Example 3:**

```
Input: s = "2[abc]3[cd]ef"
Output: "abcabccdcdcdef"
```

&#x20;

**Constraints:**

* `1 <= s.length <= 30`
* `s` consists of lowercase English letters, digits, and square brackets `'[]'`.
* `s` is guaranteed to be **a valid** input.
* All the integers in `s` are in the range `[1, 300]`.

## Solution

Algorithm

* create a stack
* add the string in reverse order to the stack so that we can get the left elements on top
* pop the stack and build a string till you find a digit
* find the length of the digit by looping till you find the whole number with all the digits
* till you find matching braces, pop elements and store them
* use the stored elements to loop through and push them to the stack
* repeat till the string contains no encoding strings&#x20;
* return the value

Use `Character.isDigit(n)` to get the boolean value

`Integer.parseInt(String.valueOf(n))` to find the value of the digit

or `num = num * 10 + c - '0';`

Edge cases&#x20;

* If the digit is more than 9 (two digits or more) - you need to pop till you find the entire element
* braces - loop till yoiu find a matching brace and brace left and brace right are equal

```java
class Solution {
    public String decodeString(String s) {
        // the major loop is to decode each sub string and push it to the stack
        // edge cases are - if the number value has more than one decimal point
            Stack<Character> stk = new Stack<>();
            StringBuilder cs = new StringBuilder();
            //push the values in reverse order on the stack so that we can get the first element on top of the stack
            for(int i = s.length() - 1; i>=0; i--){
                stk.push(s.charAt(i));
            }
            while(!stk.isEmpty()){
                // get the current character and remove it from stack
                char v = stk.pop();
                int num;

                if(Character.isDigit(v)) {
                    // string builder for loops instead of a string for memory efficency
                    StringBuilder kk = new StringBuilder();
                    kk.append(v);
                    // if the value is a digit more than one decimal point, concat the values
                    while(Character.isDigit(stk.peek())){
                        kk.append(stk.pop());
                    }
                    // parse the concated number
                    num = Integer.parseInt(kk.toString());
                    ArrayList<Character> ls = new ArrayList<>();
                    // remove the first brace
                    stk.pop();
                    int braces = 1;
                    // we add it to the list till we find a matching brace
                    while(braces > 0){
                            char m = stk.pop();
                            if(m == '[') braces++;
                            if(m == ']') braces --;
                            ls.add(m);
                    }
                    for(int w = 0; w < num; w++) {
                        // the minus 2 is to remove the brace we added in the wile loop while looking for enclosing braces
                        for(int j = ls.size() - 2; j>=0; j--){
                            // add the enclosed values inside braces k times
                            stk.push(ls.get(j));
                        }
                    }
                }
                else {
                    // otherwise the value is a string so append it
                    cs.append(v);
                }
            }
            return cs.toString();
        }

}
```

