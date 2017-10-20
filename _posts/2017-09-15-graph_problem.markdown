---
layout:     post
title:      "Graph Search: Topological Ordering"
date:       2017-09-15
author:     "BoyuanZH"
header-img: "img/post-bg-building.jpg"
tags:
    - Leetcode
    - Algorithm
    - Study Notes
---

Problem to detect acyclic directed graph or acyclic undirected graph needs the concept of topological ordering.

> 1. [207. Course Schedule](https://leetcode.com/problems/course-schedule/discuss/)

Following solution is self-explaining, but got a TLE.
 
```
 class Solution(object):
    def canFinish(self, numCourses, prerequisites):
        indegree = [0] * numCourses
        memo = [[0]*numCourses for i in range(numCourses)]
        queue = []
        
        for [ready, pre] in prerequisites:
            if memo[ready][pre] == 0: # exclude duplicated pairs.
                indegree[ready] += 1
                memo[ready][pre] = 1
        for i in range(len(indegree)):
            if indegree[i] == 0:
                queue.append(i)
                
        count = 0
        while not queue == []:
            pre = queue[0]
            queue.remove(pre)
            count += 1
            for i in range(numCourses):
                if memo[i][pre] == 1:
                    indegree[i] -= 1
                    if indegree[i] == 0:
                        queue.append(i)        
        return count == numCourses
```
 
 Solution as follow has pattern of topological ordering using DFS traversal
     
     
```
     
 class Solution(object):
    def canFinish(self, numCourses, prerequisites):
        memo = [[] for i in range(numCourses)]
        visited = [0] * numCourses
        
        # initialized the memo (graph info)
        for [ready, pre] in prerequisites:
            memo[ready].append(pre)
        
        for ready in range(len(memo)):
            for pre in memo[ready]:
                if self.isAcyclic(memo, visited, pre) == False:
                    return False
        return True
        
    def isAcyclic(self, memo, visited, pre):
        if visited[pre] == 1:
            return True
        elif visited[pre] == -1:
            return False
        else:
            visited[pre] = -1
            for prepre in memo[pre]:
                if self.isAcyclic(memo, visited, prepre) == False:
                    return False
            visited[pre] = 1
            return True
```
> 2. [10. Course Schedule II](https://leetcode.com/problems/course-schedule-ii/description/)
> 
> 3. [332. Reconstruct Itinerary](https://leetcode.com/problems/reconstruct-itinerary/description/)
 