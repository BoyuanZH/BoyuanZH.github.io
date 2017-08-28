---
layout:     post
title:      "Algorithm: Majority Voting Problem"
subtitle:   "Like a Dynamical Programming"
date:       2017-08-28
author:     "BoyuanZH"
header-img: "img/post-bg-algorithm.jpg"
tags:
    - Leetcode
    - Algorithm
    - Study Notes
---

----

# Majority Voting Algorithm

Recently I run into this kind of program in leetcode, where you want to know if there exist a value that present in an unsorted list for more than half of the elements in that list, and find it out if certain value exists. It's relatively easy to use a map to reach **O(N) time complexity and O(N) space complexity**. While, how can we reduce the **space complexity to O(1)**?

The answer is **Boyer and Moore Majority Voting Algortithm**. Check out [this helpful post](https://gregable.com/2013/10/majority-vote-algorithm-find-majority.html) for understanding the algorithm.

I'd also like to cite one post from the LC forum trying to explain the algorithm, which I think is insightful.

```
And I want to express my thinking of this solution.

When count != 0 , it means nums[1...i] has a majority,which is major in the solution.
When count == 0 , it means nums[1...i ] doesn't have a majority, so nums[1...i ] will not help nums[1...n].And then we have a subproblem of nums[i+1...n].

I think it's kind of DP.
```

> Related Problems:
> 
> 1. [169. Majority Element](https://leetcode.com/problems/majority-element/description/)
> 2. [229. Majority Element II](https://leetcode.com/problems/majority-element-ii/description/)
> 
> 
> 

