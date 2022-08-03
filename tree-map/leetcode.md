# LeetCode

### Solution

#### Solution 1

[https://leetcode.com/problems/my-calendar-i/discuss/2373132/Must-read-solution-%2B-Intuition-or-With-Image-Explanation-or-Binary-Search](https://leetcode.com/problems/my-calendar-i/discuss/2373132/Must-read-solution-%2B-Intuition-or-With-Image-Explanation-or-Binary-Search)

This post is a must read if you want to have great understanding and intuition behind intervals.

I've explained everything in detail, this is a little bit verbose but defintely worth the read.

If you found it helpful, please upvote <3

***

## Intuition

We need to manage a calendar by booking events.

We also cannot book an event if it causes a conflict. Let's define a conflict logically as:

`event1_start < event2_end AND event2_start < event1_end`

Let's visualize some interval conflicts

![image](https://assets.leetcode.com/users/images/260e87af-7f80-4a6e-bb0f-591ef6362ada\_1659513275.8805177.png)

## Brute force approach

We could insert the events into an array `events` and for every event we want to add, we would iterate that array and check for conflicts.

If no conflicts found, we can add the new event. Otherwise we can't

```
class MyCalendar:
    def __init__(self):
        self.events = []

    def book(self, start: int, end: int) -> bool:
        for event_start, event_end in self.events:
            if event_start < end and start < event_end: return False
        
        self.events.append((start, end))
        return True
```

This approach gets AC, but we can do better!

## Optimization Intuition

After playing with the input for some time, we derive an **amazing observation**

An interval (booking in our case) is defined by `start` and `end` points.

Imagine we had the current bookings: `[(2,5), (6,10)]`

We can flatten this data into a 1D array `events` where every interval is stored by first storing the `start` and then the `end` of that interval. For example with the previous booking array, we would have:

`events = 2,5,6,10`

Let's observe some properties:

1. We append an interval with 2 data points, start and end. start will always have an `even` index, while end will always have an `odd` index.
2. Start and end indexes will be adjacent. To be more specific, `start index + 1 == end index`
3. The array must be **sorted** for this properties to hold

Let's see what happens when we add 2 new intervals, 1 will conflict and the other won't.\
We want to add: `(11, 15)` (non conflicting), and `(4,7)` (conflicting).

At the moment: `events = 2,5,6,10`

Adding (11, 15) will cause the events array to become: `2,5,6,10,**11**,**15**`. All properties hold

Adding 4,7 will cause the events array to become: `2,**4**,5,6,**7**,10,11,15`.

One of the properties breaks, the indexes are not adjacent! this means we have a conflict.

So whenever we add a new interval, if the properties break, we know that interval causes a conflict.

**Approach**

1. We will insort the `start`, `end` of the interval to always have non decreasing order. This way we can perform binary search to find the insertion index
2. Because an interval is \[start, end) it means we can have `2,4,4,6`. So whenever we want to add `(4,6)` we will binary search the right-most insertion index (previous interval ended at 4, and the new interval, starting at 4 must come after that)
3. We will binary search the left-most index for end (because if there is a an interval that starts the same time previous interval ended, it must be on the right index)
4. Before inserting the `start` and `end`, both `start` and `end` insertion indexes should have the same index. Only after inserting the start and end, they will become `start_index + 1 == end_index`

## Code

```
class MyCalendar:
    def __init__(self):
        self.events = []

    def book(self, start: int, end: int) -> bool:
        start_index = bisect.bisect_right(self.events, start)
       
        # start point must have even index
        if start_index % 2 != 0: return False
        
        end_index = bisect.bisect_left(self.events, end)
        
        # Both start and end must have same index before insertion
        if end_index != start_index: return False
        
        bisect.insort_right(self.events, start)
        bisect.insort_left(self.events, end)
        return True
```



#### Solution 2



**Balanced Tree \[Accepted]**

**Intuition**

If we maintained our events in _sorted_ order, we could check whether an event could be booked in O(\log N)O(logN) time (where NN is the number of events already booked) by binary searching for where the event should be placed. We would also have to insert the event in our sorted structure.

**Algorithm**

We need a data structure that keeps elements sorted and supports fast insertion. In Java, a `TreeMap` is the perfect candidate. In Python, we can build our own binary tree structure.

For Java, we will have a `TreeMap` where the keys are the start of each interval, and the values are the ends of those intervals. When inserting the interval `[start, end)`, we check if there is a conflict on each side with neighboring intervals: we would like `calendar.get(prev)) <= start <= end <= next` for the booking to be valid (or for `prev` or `next` to be null respectively.)

For Python, we will create a binary tree. Each node represents some interval `[self.start, self.end)` while `self.left, self.right` represents nodes that are smaller or larger than the current node.



```java
class MyCalendar {
    TreeMap<Integer, Integer> calendar;

    MyCalendar() {
        calendar = new TreeMap();
    }

    public boolean book(int start, int end) {
        Integer prev = calendar.floorKey(start),
                next = calendar.ceilingKey(start);
        if ((prev == null || calendar.get(prev) <= start) &&
                (next == null || end <= next)) {
            calendar.put(start, end);
            return true;
        }
        return false;
    }
}
```

**Complexity Analysis**

* Time Complexity (Java): O(N \log N)O(NlogN), where NN is the number of events booked. For each new event, we search that the event is legal in O(\log N)O(logN) time, then insert it in O(1)O(1) time.
* Time Complexity (Python): O(N^2)O(N2) worst case, with O(N \log N)O(NlogN) on random data. For each new event, we insert the event into our binary tree. As this tree may not be balanced, it may take a linear number of steps to add each event.
* Space Complexity: O(N)O(N), the size of the data structures used.
