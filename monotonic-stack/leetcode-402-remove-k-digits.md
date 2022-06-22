# LeetCode 402 - Remove K Digits

## **Question**&#x20;

Given string num representing a non-negative integer `num`, and an integer `k`, return _the smallest possible integer after removing_ `k` _digits from_ `num`.

&#x20;

**Example 1:**

```
Input: num = "1432219", k = 3
Output: "1219"
Explanation: Remove the three digits 4, 3, and 2 to form the new number 1219 which is the smallest.
```

**Example 2:**

```
Input: num = "10200", k = 1
Output: "200"
Explanation: Remove the leading 1 and the number is 200. Note that the output must not contain leading zeroes.
```

**Example 3:**

```
Input: num = "10", k = 2
Output: "0"
Explanation: Remove all the digits from the number and it is left with nothing which is 0.
```

## **Solution**

On the above question, we  need to make note of one major detail

That is _**"A larger digit on the left side of the number is more significant than an even larger digit on the right"**_

_**e.g - Consider the number 413456 -**_ If we are asked to remove a single digit so that the resulting number is smaller, we can remove 6 (the largest number) but the position is on the right (**one's position**) so removing it wont have that much significance

But, if we remove the first 4 from the left side, we would decrement the resulting number by a large margin as the digit is in the **100000th spot**.

So considering that the removal of the digits depends on a **position**, we use a _**`monotonic stack`**_   _****_   &#x20;

> **Removing a digit/digits on the left will have more effect than removing numbers on right**&#x20;

So, in our solution, all we need to do is navigate from left to right till we find the left biggest digit from the neighbors

E.g

&#x20;`Consider the number 345362 if we want to remove 2 digits, we start from left and navigate till the element is larger than the neighbouring elements. So, in our case 5 fits the description as it is larger than the left 4 and the right 3 so we start our removal from that`

This can be easily be done with a stack as it keeps track of the last element as well as the order of elements before it

### Edge Cases

As with all leet code questions, there are some edge cases we need to consider

* _Consider the number **10** and we are asked to remove a single digit. By our code, there is no left element to check and it will not pop any element as we are comparing the last element from the current one. So it will add 1 to the stack and when trying to add 0, it will check the left and since the left is larger, it will not remove the 0 and we end up not poping any element. so in that case, it means that the elements are in decending order. So, if that is the case, we need to remove elements from the right. So in our case we just loop through and remove 1 element from the right_
* _If there are leading zeros, we remove them by looping and checking if there are leading zeros. We can convert it to string **but conversion might make us lose persision as the number might be long so better to keep it as a string**_
* _Another edge cases is, what if we remove all of the elements from the stack and we have nothing. in that case, we need to return "0"_



### Code

```java
class Solution {
    public String removeKdigits(String num, int k) {
        // Create a new stack
        Stack<Character> stk = new Stack<>();
        // change to array to compare each element
        char[] ch = num.toCharArray();
        // for each element inside the array
        for(Character c : ch) {
            // for the length of k, compare to the previous value to find the local largest value and when you find it, remove element k times
            while(k>0 && !stk.isEmpty() && stk.peek() > c) {
                stk.pop();
                k--;
            }
            stk.push(c);
        }
        // edge case 1 - if the elements are in decending order and we cant remove any element, we just pop elements from the right
        while(k>0 && !stk.isEmpty())
        {
            stk.pop();
            k--;
        }
        // we pop elements from stack and append them but mind that wil will reverse our string when poping so we need to reverse it back
        StringBuilder sb = new StringBuilder();
        while(!stk.isEmpty()){
            sb.append(stk.pop());
        }
        // reversing to get 
       sb.reverse();
        // edge case 2 - removing leading zeros
        while(sb.toString().startsWith("0")){
            sb.deleteCharAt(0);
        }
        // edge case 3 - returning "0" if the string is empty
        return sb.length() == 0 ? "0" : sb.toString();
    }
}
```
