---
layout:     post
title:      "Summary of Binary Tree Traversal"
subtitle:   " \"What info can a certain traversal provides to you?\""
date:       2017-08-12 12:00:00
author:     "BoyuanZH"
header-img: "img/home-bg1.jpg"
tags:
    - LeetCode
---

## Summary of Traversal

**What are the infomation a certain traversal provides to you?**

**How to implement a traversal?**



* preorder
* inorder
* postorder
* level

> **Related Problem**
> 
1. [105. Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/description/)
2. [106. Construct Binary Tree from Inorder and Postorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/description/)
3. [Construct BT from Inorder and Levelorder traversal](http://www.geeksforgeeks.org/construct-tree-inorder-level-order-traversals/)
4. [297. Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/description/) 
5. [114. Flatten Binary Tree to Linked List] (https://leetcode.com/problems/flatten-binary-tree-to-linked-list/description/)(The disscussion of first solution is super helpful!)
6. [230. Kth Smallest Element in a BST] (https://leetcode.com/problems/kth-smallest-element-in-a-bst/description/) (Recursive or Iterative or Binary Search)


>>*A Concise Answer for 297. Serialize and Deserialize BT:*
>>
>> ```
>> public String serialize(TreeNode root) {
    return serial(new StringBuilder(), 	root).toString();
    }
    // Generate preorder string
	private StringBuilder serial(StringBuilder str, TreeNode root) {
	    if (root == null) return str.append("#");
	    str.append(root.val).append(",");
	    serial(str, root.left).append(",");
	    serial(str, root.right);
	    return str;
	}
public TreeNode deserialize(String data) {
    return deserial(new LinkedList<>(Arrays.asList(data.split(","))));
} 
// Use queue to simplify position move
private TreeNode deserial(Queue<String> q) {
    String val = q.poll();
    if ("#".equals(val)) return null;
    TreeNode root = new TreeNode(Integer.valueOf(val));
    root.left = deserial(q);
    root.right = deserial(q);
    return root;
}
>> ```


