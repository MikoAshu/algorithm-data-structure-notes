# Guide

**A comprehensive guide and template for monotonic stack based problems**

273[![darkalarm's avatar](https://assets.leetcode.com/users/darkalarm/avatar\_1629898801.png)](https://leetcode.com/darkalarm)[darkalarm](https://leetcode.com/darkalarm)![](https://leetcode.com/static/images/badges/dcc-2022-7.png)493

Last Edit: 2 days ago

5.0K VIEWS

#### Introduction

I've had my fair share of time dealing with problem related to monotonic stack. To be honest, some of the parts have been fairly confusing. Today, I decided to address it by writing a comprehensive resource that formulises when to use monotonic stack and which templates work in which cases.

#### Problem

Monotonic stacks are generally used for solving questions of the type - next greater element, next smaller element, previous greater element and previous smaller element. We are going to create a template for each of the format, and then use them to solve variety of problems.

The template is slightly opinionated. To keep things simple, while traversing through an array, we always go from left to right. You might come across some implementations where they go from left to right for some problem and right to left for another, I feel it only adds to our confusion. Let's keep it simple.

#### Assumptions and audience

I'm assuming that you are familiar with stack data structure. You might have used them to convert recursion into iteration, expression evaluation etc. In this article, we focus on building a special type of stack - monotonic stack.

If you have dealt with questions to find next greater, previous smaller elements in an array, then this article will give you some clarity of thought process.

#### What is monotonic stack?

There could be four types of monotonic stacks. Please read them carefully, we'll refer to these types at multiple places in the sections below.

1. **Strictly increasing** - every element of the stack is strictly greater than the previous element. Example - `[1, 4, 5, 8, 9]`
2. **Non-decreasing** - every element of the stack is greater than or equal to the previous element. Example - `[1, 4, 5, 5, 8, 9, 9]`
3. **Strictly decreasing** - every element of the stack is strictly smaller than the previous element - `[9, 8, 5, 4, 1]`
4. **Non-increasing** - every element of the stack is smaller than or equal to the previous element. - `[9, 9, 8, 5, 5, 4, 1]`

We also assume that the right most element is at the top of the stack and left most element is at the bottom of the stack.

#### A generic template

We can use the following template to build a stack that keep the monotonous property alive through the execution of the program. Don't worry if you don't understand it right now, we'll be using this template later on to work on some specific examples. That might be another opportunity to understand what is happening here.

```
function buildMonoStack(arr) {
	// initialize an empty stack
	stack = [];
	
	// iterate through all the elements in the array
	for (i = 0 to arr.length - 1)) {
	  while (stack is not empty && element represented by stack top `OPERATOR` arr[i]) {
	    // if the previous condition is satisfied, we pop the top element
	    let stackTop = stack.pop();
  
	    // do something with stackTop here e.g.
	    // nextGreater[stackTop] = i
	  }
  
	  if (stack.length) {
	    // if stack has some elements left
	    // do something with stack top here e.g.
	    // previousGreater[i] = stack.at(-1)
	  }

	  // at the ened, we push the current index into the stack
	   stack.push(i);
	}
	
	// At all points in time, the stack maintains its monotonic property
}
```

**Notes about the template above**

* We initialize an empty stack at the beginning.
* The stack contains the index of items in the array, not the items themselves
* There is an outer `for` loop and inner `while` loop.
* At the beginning of the program, the stack is empty, so we don't enter the `while` loop at first.
* The earliest we can enter the `while` loop body is during the second iteration of `for` loop. That's when there is at least an item in the stack.
* At the end of the `while` loop, the index of the current element is pushed into the stack
* The `OPERATOR` inside the while loop condition decides what type of monotonic stack are we creating.
* The `OPERATOR` could be any of the four - `>, >=, <, <=`

**Time complexity** - It can be argued that no element is accessed more than four times (a constant) - one, when comparing its value with the item in the stack (`while` conditional). two, when pushing the item in the stack. three, when comparing this item in the stack with the current item being iterated (`while` conditional again). four, when popping the item out of stack. As a result, _the time complexity of this algorithm is linear._ - `O(n)` where n is the number of elements in the array.

**Space complexity** - Because we are using an external data structure - stack. In the worst can it can be filled with all the elements in the array. _The space complexity is also linear_. - `O(n)` where n is the number of elements in the array.

#### Finding next and previous, greater and smaller elements in the array

Finding next greater, previous greater, next smaller and previous smaller elements is the best showcase application of monotonic stack. Once you understand how to apply monotonics stacks for these problems, you'll be able to apply it for other variety of problems as well.

![image](https://assets.leetcode.com/users/images/3b666e9c-4200-4245-bce8-7d7e81649f8f\_1659039679.8631365.png)

In our implementation, finding next greater and previous greater elements require building a monotone decreasing stack. For finding next smaller and previous smaller requires building a monotone increasing stack. To help you remember this, think of this as an inverse relation - **greater requires decreasing, smaller requires increasing stacks**.

**1. Next Greater**

Let's start with this example. We are given with the following array and we need to find the next **greater** elements for each of items of the array.

`arr` = `[13, 8, 1, 5, 2, 5, 9, 7, 6, 12]`

Next greater elements (what is the next greater element for the item at this index) -\
`nextGreaterElements` = `[null, 9, 5, 9, 5, 9, 12, 12, 12, null]`

On the place of writing the element itself, we can also write its index -\
`nextGreaterIndexes` = `[-1, 6, 3, 6, 5, 6, 9, 9, 9, -1]` (for 13 and 12, because there are no greater elements after themselves, we use -1, an invalid index value of the next greater element. You could use `null` or `arr.length` as well.

Let's use the template given above to solve this question. The following code uses the template and implement next greater element program. Please read the comments in the code to understand what we are doing on these lines.

```
function findNextGreaterIndexes(arr) {
  // initialize an empty stack
  let stack = [];
  
  // initialize nextGreater array, this array hold the output
  // initialize all the elements are -1 (invalid value)
  let nextGreater = new Array(arr.length).fill(-1);
  
  // iterate through all the elements of the array
  for (let i = 0; i < arr.length; i++) {
  
    // while loop runs until the stack is not empty AND
    // the element represented by stack top is STRICTLY SMALLER than the current element
    // This means, the stack will always be monotonic non increasing (type 4)
    while (stack.length && arr[stack.at(-1)] < arr[i]) {
    
      // pop out the top of the stack, it represents the index of the item
      let stackTop = stack.pop();
      
      // as given in the condition of the while loop above,
      // nextGreater element of stackTop is the element at index i
      nextGreater[stackTop] = i;
    }
    
    // push the current element
    stack.push(i);
  }
  return nextGreater;
}
```

**Notes**

1. For finding next greater elements (not equal) we use a monotonic non increasing stack (type 4)
2. If the question was to find next `greater or equal` elements, then we would have used a monotonic strictly decreasing stack (type 3)
3. We use the operator `<` in while loop condition above - this results in a monotonic non increasing stack (type 4). If we use `<=` operator, then this becomes a monotonic strictly decreasing stack (type 3)
4. Time and space complexity - `O(n)`

**2. Previous Greater**

This time we want to find the previous greater elements. One option is to iterate from `arr.length - 1` to `0` and use the same logic as above in the opposite direction. In order to keep things simple, I rather like another flavour of the template above where we add three more lines after the `while` loop to get the previous greater element. Let's see how to do that.

`arr` = `[13, 8, 1, 5, 2, 5, 9, 7, 6, 12]`

Previous greater elements -\
`previousGreaterElements` = `[null, 13, 8, 8, 5, 8, 13, 9, 7, 13]`\
`nextGreaterIndexes` = `[-1, 0, 1, 1, 3, 1, 0, 6, 7, 0]`

```
function findPreviousGreaterIndexes(arr) {
	// initialize an empty stack
	let stack = [];
	
	// initialize previousGreater array, this array hold the output
	// initialize all the elements are -1 (invalid value)
	let previousGreater = new Array(arr.length).fill(-1);
	
	// iterate through all the elements of the array
	for (let i = 0; i < arr.length; i++) {
	
	   // while loop runs until the stack is not empty AND
	   // the element represented by stack top is SMALLER OR EQUAL to the current element
	   // This means, the stack will always be strictly decreasing (type 3) - because elements are popped when they are equal
	   // so equal elements will never stay in the stack (definition of strictly decreasing stack)
		while (stack.length && arr[stack.at(-1)] <= arr[i]) {
		
			// pop out the top of the stack, it represents the index of the item
			let stackTop = stack.pop();
		}
		
		// after the while loop, only the elements which are greater than the current element are left in stack
		// this means we can confidentally decide the previous greater element of the current element i, that's stack top
		if (stack.length) {
			previousGreater[i] = stack.at(-1);
		}
		
		// push the current element
		stack.push(i);
	}
	return previousGreater;
}
```

**Notes**

1. For finding previous greater elements (not equal) we use a monotonic strictly decreasing stack (type 3)
2. If the question was to find previous `greater or equal` elements, then we would have used a monotonic non increasing stack (type 4)
3. We use the operator `<=` in while loop condition above - this results in a monotonic strictly decreasing stack (type 3). If we use `<` operator, then this becomes a monotonic non increasing stack (type 4).
4. Time and space complexity - `O(n)`

**3. Next Greater and Previous Greater at the same time**

If we merge the code from heading (1) and (2) both above, we can get next greater and previous greater from the same program. There is only one limitation.\
One of previousGreater or nextGreater won't be strictly greater (but greater or equal). If this satisfies our requirement, we can use the following solution.

For example, in the array `[13, 8, 1, 5, 2, 5, 9, 7, 6, 12]`\
The next greater element for the first `5` will be `9`, the previous greater element for the second `5` will be `5` (not `8`)\
OR\
The next greater element for the first `5` will be `5` (not `9`), the previous greater element for the second `5` will be `8`.

This solution works if you are okay with one of the two cases above. Let's look at the code now.

```
function findNextAndPreviousGreaterIndexes(arr) {
  // initialize an empty stack
  let stack = [];
  
  // initialize previousGreater and nextGreater arrays
  let previousGreater = new Array(arr.length).fill(-1);
  let nextGreater = new Array(arr.length).fill(-1);
  
  // iterate through all the elements of the array
  for (let i = 0; i < arr.length; i++) {
  
     // while loop runs until the stack is not empty AND
     // the element represented by stack top is SMALLER OR EQUAL to the current element
     // This means, the stack will always be strictly decreasing (type 3) - because elements are popped when they are equal
     // so equal elements will never stay in the stack (definition of strictly decreasing stack)
    while (stack.length && arr[stack.at(-1)] <= arr[i]) {
    
      // pop out the top of the stack, it represents the index of the item
      let stackTop = stack.pop();
      
      // This is the only additional line added to the last approach
      // decides the next greater element for the index popped out from stack
      nextGreater[stackTop] = i;
    }
    
    // after the while loop, only the elements which are greater than the current element are left in stack
    // this means we can confidentally decide the previous greater element of the current element i, that's stack top
    if (stack.length) {
      previousGreater[i] = stack.at(-1);
    }
    
    // push the current element
    stack.push(i);
  }
  return [previousGreater, nextGreater];
}
```

**Note**: In the code example given above, the `nextGreater` array points at next **greater or equal** element. While `previousGreater` array points at **strictly greater** elements in the leftward direction (previous strictly greater).

**4. Next Smaller (strictly smaller)**

If you have were able to understand the logic until this point, finding next smaller and previous smaller shouldn't be difficult at all. To get previous greater elements we simply flip the operator from `<` to `>`. By doing this we end up creating a strictly increasing (type 1) or a non-decreasing (type 2) array. Given that I've already explained the corresponding cases for next greater and previous greater elements, let me directly show you code examples below.

```
function findNextSmallerIndexes(arr) {
  // initialize an empty stack
  let stack = [];
  
  // initialize nextGreater array, this array hold the output
  // initialize all the elements are -1 (invalid value)
  let nextSmaller = new Array(arr.length).fill(-1);
  
  // iterate through all the elements of the array
  for (let i = 0; i < arr.length; i++) {
  
    // while loop runs until the stack is not empty AND
    // the element represented by stack top is STRICTLY LARGER than the current element
    // This means, the stack will always be monotonic non decreasing (type 2)
    while (stack.length && arr[stack.at(-1)] > arr[i]) {
    
      // pop out the top of the stack, it represents the index of the item
      let stackTop = stack.pop();
      
      // as given in the condition of the while loop above,
      // nextSmaller element of stackTop is the element at index i
      nextSmaller[stackTop] = i;
    }
    
    // push the current element
    stack.push(i);
  }
  return nextSmaller;
}
```

**5. Previous Smaller (strictly smaller)**

```
function findNextSmallerIndexes(arr) {
  // initialize an empty stack
  let stack = [];
  
  // initialize previousSmaller array, this array hold the output
  // initialize all the elements are -1 (invalid value)
  let previousSmaller = new Array(arr.length).fill(-1);
  
  // iterate through all the elements of the array
  for (let i = 0; i < arr.length; i++) {
  
    // while loop runs until the stack is not empty AND
    // the element represented by stack top is LARGER OR EQUAL to the current element
    // This means, the stack will always be monotonic strictly increasing (type 1)
    while (stack.length && arr[stack.at(-1)] >= arr[i]) {
    
      // pop out the top of the stack, it represents the index of the item
      let stackTop = stack.pop();
    }
    
    // this is the additional bit here
    if (stack.length) {
      // the index at the stack top refers to the previous smaller element for `i`th index
      previousSmaller[i] = stack.at(-1);
    }
    
    // push the current element
    stack.push(i);
  }
  return previousSmaller;
}
```

**6. Next Smaller and Previous Smaller (merged, one strictly smaller, and the other smaller or equal)**

```
function findNextSmallerIndexes(arr) {
  // initialize an empty stack
  let stack = [];
  
  // initialize previousSmaller array, this array hold the output
  // initialize all the elements are -1 (invalid value)
  let previousSmaller = new Array(arr.length).fill(-1);
  
  // iterate through all the elements of the array
  for (let i = 0; i < arr.length; i++) {
  
    // while loop runs until the stack is not empty AND
    // the element represented by stack top is LARGER OR EQUAL to the current element
    // This means, the stack will always be monotonic strictly increasing (type 1)
    while (stack.length && arr[stack.at(-1)] >= arr[i]) {
    
      // pop out the top of the stack, it represents the index of the item
      let stackTop = stack.pop();
      
      // as given in the condition of the while loop above,
      // nextSmaller element of stackTop is the element at index i
      nextSmaller[stackTop] = i;
    }
    
    // this is the additional bit here
    if (stack.length) {
      // the index at the stack top refers to the previous smaller element for `i`th index
      previousSmaller[i] = stack.at(-1);
    }
    
    // push the current element
    stack.push(i);
  }
  return [nextSmaller, previousSmaller];
}
```

#### Summary

Let's summarize all the approaches here, to cement our learning.

| Problem          | Stack Type                 | Operator in while loop | Assignment Position |
| ---------------- | -------------------------- | ---------------------- | ------------------- |
| next greater     | decreasing (equal allowed) | stackTop < current     | inside while loop   |
| previous greater | decreasing (strict)        | stackTop <= current    | outside while loop  |
| next smaller     | increasing (equal allowed) | stackTop > current     | inside while loop   |
| previous smaller | increasing (strict)        | stackTop >= current    | outside while loop  |

Let's apply our newly learned knowledge at some problems now.

#### Problems

[**503: Next Greater Element II**](https://leetcode.com/problems/next-greater-element-ii/)

It is essentially the same problem as the one described above. There is an additional twist of being a circular array. Which means, the next greater element for the last element in the array could be the first of the previous elements if it is bigger. (the array wraps around)

To solve this problem, we run the parent `for` loop two times.

```
function nextGreaterCircular(arr) {
  let nextGreater = new Array(arr.length).fill(-1);
  let stack = [];
  // run the outer loop two times
  for (let j = 0; j < 2 ; j++) {
    // this is same as discussed above in the template
    for (let i = 0; i < arr.length; i++) {
      while (stack.length && arr[stack.at(-1)] < arr[i]) {
        let stackTop = stack.pop();
      nextGreater[stackTop] = arr[i];
      }
      stack.push(i);
    }
  }
  return nextGreater;
}
```

[**739: Daily Temperatures**](https://leetcode.com/problems/daily-temperatures/)

This is next greater question in disguise of daily temperatures.

```
function dailyTemperatures(temperatures) {
  // asking for next greater (strict)
  let stack = [];
  let nextGreater = new Array(temperatures.length).fill(0);
  for (let i = 0; i < temperatures.length; i++) {
    // next greater (strict) => non-increasing monotonic stack 
    // strict => operator is going to be '<'
    while (stack.length && temperatures[stack.at(-1)] < temperatures[i]) {
      let stackTop = stack.pop();
      // i - stackTop is the number of days to wait
      nextGreater[stackTop] = i - stackTop;
    }
    stack.push(i);
  }
  return nextGreater;
};
```

[**1762: Buildings with an ocean view**](https://leetcode.com/problems/buildings-with-an-ocean-view/)

A building has ocean view if all buildings on its right are smaller than this building.

Problem type - `next greater`\
Stack type - `monotonic strictly decreasing`\
Operator - `<=`\
No assignment or processing step required

Read the comments in the program to understand the solution below.

```
function findBuildings(heights) {
  // in other words, we want to find which of the buildings
  // have a next greater element
  // at the end, the elements left in the stack will be the ones
  // which wouldn't have any greater elements after them
  let stack = [];
  for (let i = 0; i < heights.length; i++) {
    // note the operator used is <=
    // because we want to pop out the buildings which have another
    // building with equal or greater height in view
    // this means the monotonic stack is going to be strictly decreasing
    while (stack.length && heights[stack.at(-1)] <= heights[i]) {
      stack.pop();
    }
    stack.push(i);
  }
  return stack;
};
```

[**456: Find 132 Pattern**](https://leetcode.com/problems/132-pattern/)

I found this question to be very interesting. I would recommend trying it on your own before looking at the solution here.\
The question wants to find a triplet of three numbers from an array such that their indices and numbers fulfill this condtion - `i < j < k` and `arr[i] < arr[k] < arr[j]`\
You can see that we are making a pattern like `1 - 3 - 2`

Alternate way of asking the same question -

1. Find previous greater element for each number `a`.
2. Once the previous greater element `x` is found, check the previous minimum element for `x`
3. If the previous minimum number is smaller than the number `a`, we know the pattern exists

We'll need to preprocess `minimum encountered till now` for each of the numbers in the array.

```
function find132pattern(nums) {
  let minimums = new Array(nums.length).fill(0);
  let stack = [];
  
  for (let i = 0; i < nums.length; i++) {    
    // setup minimums
    if (i === 0) {
      minimums[i] = 0;
    } else {
      if (nums[i] < nums[minimums[i - 1]]) {
        minimums[i] = i;
      } else {
        minimums[i] = minimums[i - 1];
      }
    }
    
	// using template for finding previous greater elements
	
    // find previous greater element, build monotonic decreasing stack
    while (stack.length && nums[stack.at(-1)] <= nums[i]) {
      let stackTop = stack.pop();
    }
    
    // if there is a previous greater element, stack will not be empty
    if (stack.length) {
      // if the previous minimum for the previous greater element is
      // less than the current number, then we return true
      if (nums[minimums[stack.at(-1)]] < nums[i]) {
        return true;
      }
    }
    stack.push(i);
  }
  
  return false;
};
```

[**42: Trapping rain water**](https://leetcode.com/problems/trapping-rain-water/)

For this question, we are using a modified version of next greater element template.

1. We use a strictly decreasing monotonic stack here.
2. The inside of while loop is a bit involved. When we do `stack.pop()`,\
   we know that `element i` (current element) is larger than or equal to the element at stack top.\
   In other words, if we are focusing at the `stackTop` element, we know its next greater element is at index `i`
3. Inside the `while` loop, if the stack is not empty, the previous element in the stack is the previous greater element to this one (`stackTop`).
4. With the next greater and previous greater element available for `stackTop`, we can calculate the water fill.

```
var trap = function(height) {
  let stack = [];
  let count = 0;
  for (let i = 0; i < height.length; i++) {
    while (stack.length && height[stack.at(-1)] <= height[i]) {
      let stackTop = stack.pop();
      if (stack.length) {
	    // h (height) is the minimum of the previous greater or the next greater elements
        let h = Math.min(height[stack.at(-1)], height[i]) - height[stackTop];
		
		// w (width) is the space between next greater and previous greater element
        let w = i - (stack.at(-1) + 1);
		
		// h * w is the area this stackTop contributes
        count += h * w;
      }
    }
    stack.push(i);
  }
  return count;
};
```

[**84: Largest rectangle in histogram**](https://leetcode.com/problems/largest-rectangle-in-histogram/)

The solution for this question uses template 6 above. We merge the solution for previous smaller and next smaller both.\
In the example below, `nextSmaller` is strictly smaller while `previousSmaller` also considers equal elements (in addition to smaller elements).\
This actually works in our favour because this is making sure we don't count the same element twice.

```
function largestRectangleArea(heights) {
  let nextSmaller = new Array(heights.length).fill(heights.length);
  let previousSmaller = new Array(heights.length).fill(-1);
  let stack = [];
  
  // calculate previousSmaller and nextSmaller both
  for (let i = 0; i < heights.length; i++) {
    while (stack.length && heights[stack.at(-1)] > heights[i]) {
      let stackTop = stack.pop();
      nextSmaller[stackTop] = i;
    }
    if (stack.length) {
      previousSmaller[i] = stack.at(-1);
    }
    stack.push(i);
  }
  
  let maxArea = 0;
  for (let i = 0; i < heights.length; i++) {
    let currentHeight = heights[i];
    let width = nextSmaller[i] - previousSmaller[i] - 1;
    maxArea = Math.max(maxArea, currentHeight * width);
  }
  
  return maxArea;
};
```

#### Conclusion

If you have made it till this point, congratulations, you have graduated in the topic of monotonic stack. To practice more monotonic stack based problems on LeetCode, you can refer to this [tag page](https://leetcode.com/tag/monotonic-stack/). If you have any questions, please post them in the comments below and I'll try my best to answer them.
