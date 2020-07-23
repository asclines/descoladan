---
layout: blog
title: Maximum Subarray
description: https://leetcode.com/problems/maximum-subarray/
date: 2020-07-22T23:01:27.909Z
---
## Problem Statement
This problem comes from [LeetCode](https://leetcode.com/problems/maximum-subarray/).

Given an integer array `input`, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

**Example:**

```
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6
```  


## Walkthrough

#### Understanding the problem statement
First thing we want to do is confirm we understand the problem, it's constraints and what is expected. For example, while this problem is called "Maximum Subarray" and seems oriented around the concept of "subarray", we really only need the sum. Not needing to track what the actual subarray simplifies our work some.

This is a relatively straightforward problem statement, but not without it's edge cases. 
There is one phrase "containing at least one number" we need to remember. What if our solution contained:
```
largest_sum = 0;
for subarray in possible_subarrays:
  if sum(subarray) > largest_sum:
    largest_sum = sum(subarray)
 return largest_sum

``` 
See a problem? What if your input was `[-1,-1,-1]`? This solution would return 0 not -1. Depending on how we develop our solution this edge case may trip us up.

### Now, let's get to solving this problem.


At first thought, we might consider generating all spans of subarrays and finding their maxes. There are n(n+1)/2 subarrays which gives us a O(n^2) time complexity. Depending on how these arrays are stored we could an unpleasant space complexity as well.

There are certain optimizations one might be able to think of involving early stoppage and whatnot. However, that could lead to some ugly code and still our Big-O would be still be O(n^2) at worst case. So let's keep thinking.

From the problem statement, since we are given no constraints on ordering of numbers we have to assume the worst case is when the entire array is a contiguous subarray. Thus our solution needs to be at least linear.
Additionally we also need to consider saving results from previous computations. For example [1,2] and [1,2,3] both involve summing 1 and 2. 

When I think linear, I think iterative. Approaching this problem iteratively left to right, with a smaller example `[2,-1,3]`, let's track max numbers.

* When looking at sub-array [2] the max is 2.  
* When looking at sub-array [2,-1] we have a dilemma. 2 + -1 = 1. We know that we have a max of 2 from the previous step. So if we are looking at this greedily we might discard and start over at the next point. However we can see that the max will be 4 using the whole array so this step is actually the right direction.   
* What we need is a way to store our previous max. This will also allow us to store results from previous computations.

We can accomplish this using another list, `maxes`, for storing previous maxes. More specifically `maxes[i]` holds the largest sum seen up to `i` in `input`.  

Let's see it in action. 

`input: [-2,1,2,3,-1]`  
`maxes: [ 0,0,0,0,0]`  

We can go ahead and initialize `maxes[0]` to `input[0]` as that is the max to that point.  

`maxes: [-2,0,0,0,0]` 

For each of the following elements of `input` we want to know two things:  
1) What was the previous max before we included this index?  
2) What is the value of this element?
3) Is this element better off not using the previous max? aka what is better, `input[i]` or `maxes[i-1] + input[1]`?

 
Starting with case`i = 1`:  
1) Previous max: `maxes[i-1] = -2` . 
2) Current value: `input[i] = 1`
3) Combined: `maxes[i-1] + input[i] = -1`

The previous max hurts us so let's not use it and set `maxes[i] = 1`.

`maxes: [-2,1,0,0,0]`

Case `i = 2`:     
1) Previous max: `maxes[i-1] = 1`  
2) Current value: `input[i] = 2`
3) Combined: `maxes[i-1] + input[i] = 3`

 
In this case the previous max helps us so let's use it and set `maxes[1] = 3`.

`maxes: [-2,1,3,0,0]`


Case `i = 3`:  
1) Previous max: `maxes[i-1] = 3`  
2) Current value: `input[i] = 3`
3) Combined: `maxes[i-1] + input[i] = 6`
 
In this case the previous max helps us so let's use it and set `maxes[i] = 6`.

`maxes: [-2,1,3,6,0]`

Final case `i = 4`:  
1) Previous max: `maxes[i-1] = 6`  
2) Current value: `input[i] = -1`
3) Combined: `maxes[i-1] + input[i] = 5`


`maxes: [-2,1,3,6,5]`

At this point we have now have a lovely list of possible maxes for this array. We simply need to take the max value from this list and we have our answer.

So our algorithm becomes:
```
maxes[0] = input[0]
for i in [1 ... n-1]:
  maxes[i] = max(input[i], input[i] + maxes[i-1]
return max(maxes)

```

**Time Complexity: _O(n)_** Note that there are two linear segments, the `for` loop and the final `max` call. This is an excellent time to point out that you should be aware of space/time complexities of built in libraries you use.  
**Space Complexity: _O(n)_** since we create a new list maxes.  


### Follow up questions

#### Less Space
So now that we have a solution that is acceptable. As we inferred earlier, linear is as good as we can expect. But what about space? If you have time in an interview, the interviewer might have a follow up challenge for you; your solution must be O(1) space complexity.

So how do we do this? Well given we only have one data structure that grows linearly with the input, `maxes` that is where we need to look. Two possible solutions come to mind:
1) Is there a way to reuse the `input` data?
2) Is there a way to use a single variable to hold previous maxes? 

IDK about you but I can't think of a way to accomplish number 2, so let's assume interviewer says your `input` variable is mutable. Meaning you can modify it. Looking back at our algorithm we can see that we only use `input[i]` at `i`. More importantly, we never "look back". So we can use `input` as our `maxes` list as well. Thus we get:

```
for i in [1 ... n-1]:
  input[i] = max(input[i], input[i] + input[i-1]
return max(maxes)
```

**Time Complexity: _O(n)_**   
**Space Complexity: _O(1)_** .


For an added bonus, we can skip the second linear call by tracking `largest_sum` along the way:

```
largest_sum = input[0]
for i in [1 ... n-1]:
  input[i] = max(input[i], input[i] + input[i-1]
  largest_sum = max(largest_sum, input[i])
return largest_sum
``` 

But this change doesn't affect space/time complexities.

#### Divide n' Conquer
The LeetCode problems statement offers this as a follow up. Since this would be less efficient than solution derived above, I'm not gonna worry about it for now. Perhaps in the future I'll write up something. 

## Conclusion
For those who are familiar with advanced algorithms they might have recognized this as Kadane's algorithm. This algorithm is a staple algorithm in Computer Vision for problems like detecting brightest parts of a picture. It's also a nice introduction to thinking about problems through dynamic programming. 

Hope this helps!

