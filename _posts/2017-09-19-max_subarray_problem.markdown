---
layout:     post
title:      "Kadane's Algorithm: Maximum Subarray Problem"
subtitle:   "Like a Dynamical Programming"
date:       2017-09-19
author:     "BoyuanZH"
header-img: "img/post-bg-building.jpg"
tags:
    - Leetcode
    - Algorithm
    - Study Notes
---

> Resources:
> 
> 1. [Wiki Explanation](https://en.wikipedia.org/wiki/Maximum_subarray_problem)

> Problem using Dynamic Programming to save time:
> 
> 1. [53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/description/)
> 2. [121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/discuss/)
> 3. [122. Best Time to Buy and Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/description/)
> 3. [152. Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/description/)
> 4. [198. House Robber](https://leetcode.com/problems/house-robber/description/)
> 5. [213. House Robber II](https://leetcode.com/problems/house-robber-ii/description/)
> 6. [276. Paint Fence](https://leetcode.com/problems/paint-fence/discuss/)
> 
> 
> 
> Problem like trapping water:
> 
> 1. [42. Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/description/)
> 2. [11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/description/)
> 3. [407. Trapping Rain Water II](https://leetcode.com/problems/trapping-rain-water-ii/discuss/)
> 4. [238. Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/description/)
> 
> 
> Problem using buckets check:
> 
> 1. [220. Contains Duplicate III](https://leetcode.com/problems/contains-duplicate-iii/description/)
> 6. [204. Count Primes](https://leetcode.com/problems/count-primes/description/)
> 
> 
> 
> Problem using factors:
> 
> 1. [172. Factorial Trailing Zeroes](https://leetcode.com/problems/factorial-trailing-zeroes/description/)
> 2. 
> 
> Prolbem using elegant pointer solution:
> 
> 1. [160. Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/description/)
> 2. [26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/)
> 3. [328. Odd Even Linked List](https://leetcode.com/problems/odd-even-linked-list/description/)
> 4. [223. Rectangle Area](https://leetcode.com/problems/rectangle-area/description/)
> 5. [28. Implement strStr()](https://leetcode.com/problems/implement-strstr/description/)
> 6. [566. Reshape the Matrix](https://leetcode.com/problems/reshape-the-matrix/discuss/)
> 7. [243. Shortest Word Distance](https://leetcode.com/problems/shortest-word-distance/description/)
> 8. [447. Number of Boomerangs](https://leetcode.com/problems/number-of-boomerangs/description/)
> 9. [276. Paint Fence](https://leetcode.com/problems/paint-fence/discuss/)
> 10. [438. Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/discuss/) (Love this Problem, good template)
> 11. [455. Assign Cookies](https://leetcode.com/problems/assign-cookies/discuss/)
> 12. [475. Heaters](https://leetcode.com/problems/heaters/discuss/)
> 13. [599. Minimum Index Sum of Two Lists](https://leetcode.com/problems/minimum-index-sum-of-two-lists/description/)
> 14. [633. Sum of Square Numbers](https://leetcode.com/problems/sum-of-square-numbers/description/)
> 15. [246. Strobogrammatic Number](https://leetcode.com/problems/strobogrammatic-number/discuss/)
> 16. [594. Longest Harmonious Subsequence](https://leetcode.com/problems/longest-harmonious-subsequence/description/)
> 17. [598. Range Addition II](https://leetcode.com/problems/range-addition-ii/description/)
> 18. [581. Shortest Unsorted Continuous Subarray](https://leetcode.com/problems/shortest-unsorted-continuous-subarray/description/)
> 19. [624. Maximum Distance in Arrays](https://leetcode.com/problems/maximum-distance-in-arrays/description/)
> 20. [228. Summary Ranges](https://leetcode.com/problems/summary-ranges/discuss/)
>
> 
> Problem using stack:
> 
> 1. [150. Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/discuss/)
> 
> 
> 
> 
> Problem using lambda expression:
> 
> 1. [56. Merge Intervals](https://leetcode.com/problems/merge-intervals/description/)
> 2. [179. Largest Number](https://leetcode.com/problems/largest-number/description/)
> 
> 
> 
> Problem use matrix/array indexing tricks:
> 
> 1. [48. Rotate Image](https://leetcode.com/problems/rotate-image/discuss/)
> 2. [419. Battleships in a Board](https://leetcode.com/problems/battleships-in-a-board/description/)
> 3. [242. Valid Anagram](https://leetcode.com/problems/valid-anagram/description/)
> 4. [657. Judge Route Circle](https://leetcode.com/problems/judge-route-circle/description/)
> 5. [345. Reverse Vowels of a String](https://leetcode.com/problems/reverse-vowels-of-a-string/description/) (Reversal is all about swap. Two pointer problem)
> 6. [414. Third Maximum Number](https://leetcode.com/problems/third-maximum-number/discuss/)
> 
> Problem using recursion:
> 
> 6. [669. Trim a Binary Search Tree](https://leetcode.com/problems/trim-a-binary-search-tree/discuss/)
> 
> Problem use resversal:
> 
> 1. [190. Reverse Bits](https://leetcode.com/problems/reverse-bits/description/)
> 
> 
> Problem using the idea of data engineering:
> 
> 1. [350. Intersection of Two Arrays II](https://leetcode.com/problems/intersection-of-two-arrays-ii/description/)
> 
> 
> 
> Problem with easy logic but tricky with details.
>
>1. [69. Sqrt(x)](https://leetcode.com/problems/sqrtx/description/)
>2. [168. Excel Sheet Column Title](https://leetcode.com/problems/excel-sheet-column-title/description/)
>3. [203. Remove Linked List Elements](https://leetcode.com/problems/remove-linked-list-elements/discuss/)
>4. [476. Number Complement](https://leetcode.com/problems/number-complement/discuss/)
>5. [374. Guess Number Higher or Lower](https://leetcode.com/problems/guess-number-higher-or-lower/description/)
>6. [278. First Bad Version](https://leetcode.com/problems/first-bad-version/description/)
>7. [83. Remove Duplicates from Sorted List](https://leetcode.com/problems/remove-duplicates-from-sorted-list/discuss/)
>8. [35. Search Insert Position](https://leetcode.com/problems/search-insert-position/description/)
>9. [367. Valid Perfect Square](https://leetcode.com/problems/valid-perfect-square/discuss/)
>10. [414. Third Maximum Number](https://leetcode.com/problems/third-maximum-number/discuss/)
>11. [475. Heaters](https://leetcode.com/problems/heaters/discuss/)
>12. [680. Valid Palindrome II](https://leetcode.com/problems/valid-palindrome-ii/discuss/)
>13. [422. Valid Word Square](https://leetcode.com/problems/valid-word-square/discuss/)
>14. [408. Valid Word Abbreviation](https://leetcode.com/problems/valid-word-abbreviation/discuss/)
>15. [604. Design Compressed String Iterator](https://leetcode.com/problems/design-compressed-string-iterator/description/)
>
>Problem using math tricks:
>
>1. [453. Minimum Moves to Equal Array Elements](https://leetcode.com/problems/minimum-moves-to-equal-array-elements/description/)
>2. [400. Nth Digit](https://leetcode.com/problems/nth-digit/discuss/)
>3. [459. Repeated Substring Pattern](https://leetcode.com/problems/repeated-substring-pattern/description/)
>
>Design Problem:
>
>1. [170. Two Sum III - Data structure design](https://leetcode.com/problems/two-sum-iii-data-structure-design/description/)
>2. []()
>
> Problem might fool you:
> 
> 1. [521. Longest Uncommon Subsequence I](https://leetcode.com/problems/longest-uncommon-subsequence-i/description/)
> 2. [605. Can Place Flowers](https://leetcode.com/problems/can-place-flowers/description/)
> 3. [665. Non-decreasing Array](https://leetcode.com/problems/non-decreasing-array/description/)
> 
> 
> 
> Bit Manipulation:
> 
> 1. [405. Convert a Number to Hexadecimal](https://leetcode.com/problems/convert-a-number-to-hexadecimal/description/)
> 
> 
> Tree Travesal:
> 
> 1. [671. Second Minimum Node In a Binary Tree](https://leetcode.com/problems/second-minimum-node-in-a-binary-tree/description/)
> 
> 
> SQL:
> 
> 1. [603. Consecutive Available Seats](https://leetcode.com/problems/consecutive-available-seats/discuss/)
> 
> ----
> 
> Elegant Solution:
> 
> 1. [2. Add Two Numbers](https://leetcode.com/problems/add-two-numbers/description/)
> 2. 