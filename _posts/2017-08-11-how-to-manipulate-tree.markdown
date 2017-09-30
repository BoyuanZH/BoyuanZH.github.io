---
layout:     post
title:      "How to manipulate tree structure?"
date:       2017-08-12
author:     "BoyuanZH"
header-img: "img/post-bg.jpg"
tags:
    - LeetCode
---

## How to manipulate tree structure?
```
def connect(self, root):
    while (not root == None):
        preRoot = TreeLinkNode(0)
        curr = preRoot
        while (not root == None):
            if not root.left == None: curr.next = root.left; curr = curr.next
            if not root.right == None: curr.next = root.right; curr = curr.next
            root = root.next
        #update root:
        root = preRoot.next
```
Above is a elegent solution for [LC117: Populating Next Right Pointers in Each Node II](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/description/). For me, it is still hard to manipulate elegent **pointers** in the iterative problem of Tree structure.

**Another example of using queue in a traverse a tree:** [101. Symmetric Tree](https://leetcode.com/problems/symmetric-tree/description/)

```
def isSymmetric(self, root):
    # iteration
    if root == None: return True
    queue = []
    queue.append((root.left, root.right))
    while (not queue == []):
        (left, right) = queue[0]; queue = queue[1:]
        if right == None and left == None:
            continue
        elif (right == None or left == None) or (not right.val == left.val):
            return False
        else:
            queue += [(left.left, right.right), (left.right, right.left)]
    return True
```

Recursive Solution:

```
def isSymmetric(self, root):
    ## recursion
    return root == None or self.isSymPair(root.left, root.right)
def isSymPair(self, n1, n
2):
    if n1 == None and n2 == None:
        return True
    elif (n1 == None or n2 == None) or (not n1.val == n2.val):
        return False
    else:
        return self.isSymPair(n1.left, n2.right) and self.isSymPair(n1.right, n2.left)
```

## Optimization

**Inorder Successor in BST:**


```
def inorderSuccessor(self, root, p):
    s = None
    curr = root
    while (not curr == None):
        if p.val == curr.val:
            if not curr.right == None:
                s = self.findMin(curr.right)
            break
        elif p.val < curr.val:
            s = curr
            curr = curr.left
        else:
            curr = curr.right
    return s
    
def findMin(self, node):
    if node.left == None: return node
    return self.findMin(node.left)
```     
This [285. Inorder Successor in BST](https://leetcode.com/problems/inorder-successor-in-bst/discuss/) can be optimized as follow:

```
def inorderSuccessor(self, root, p):
	succ = None
	while root:
	    if p.val < root.val:
	        succ = root
	        root = root.left
	    else:
	        root = root.right
	return succ
```

---

**Closet BST Value**

```
def closestValue(self, root, target):
    if (root == None): return None;
    curr = root
    next = root
    minDistance = float("inf")
    closetV = curr.val
    while (not next == None):
        curr = next
        minDistance = min(minDistance, abs(target - curr.val))
        closetV = curr.val if minDistance == abs(target - curr.val) else closetV
        next = next.left if next.val > target else next.right
    return closetV if min(minDistance, abs(target - curr.val)) == minDistance else curr.val
```

This [270. Closest Binary Search Tree Value](https://leetcode.com/problems/closest-binary-search-tree-value/discuss/) can be optimized as follow:

```
def closestValue(self, root, target):
    closest = root.val
    while root:
        closest = min((root.val, closest), key=lambda x: abs(target - x))
        root = root.left if target < root.val else root.right
    return closest
```
Following answer is good for understanding the problem， O(N) space.

```
def closestValue(self, root, target):
    path = []
    while root:
        path += root.val,
        root = root.left if target < root.val else root.right
    return min(path[::-1], key=lambda x: abs(target - x))
```
## The essence of recursion: Stack (Tree Traversal)

IF necessary, also check [this version of TreeTraversal](https://leetcode.com/problems/binary-tree-postorder-traversal/discuss/).

---
**Recursive version** of Inorder Traversal

```
def inorderTraversal(self, root):
    if root == None: return []
    return self.inorderTraversal(root.left) + [root.val] + self.inorderTraversal(root.right)
```
**Iterative version** of Inorder Traversal

```
def inorderTraversal(self, root):
    if root == None: return []
    result = []
    stack = []
    while (not root == None):
        stack.append(root)
        root = root.left
    ## got all stack.peek() as the next subject to print
    while (not stack == []):
        curr = stack[-1]
        stack = stack[:-1]
        result.append(curr.val)
        if not curr.right == None:
            curr = curr.right
            while (not curr == None):
                stack.append(curr)
                curr = curr.left
    return result
```

Iterative version can be optimized as follow:

```
def inorderTraversal(self, root):
    curr = root
    stack = []
    res = []
    while not (curr == None and stack == []):
        while not curr == None:
            stack.append(curr)
            curr = curr.left
        curr = stack.pop()
        res.append(curr.val)
        curr = curr.right
    return res
```

---
**Recursive version** of Preorder Traversal

```
def preorderTraversal(self, root):
    if root == None: return []
    return [root.val] + self.inorderTraversal(root.left) + self.inorderTraversal(root.right)
```

**Iterative version** of Preorder Traversal

```
def preorderTraversal(self, root):
    if root == None: return []
    result = []
    stack = [root]
    while (not stack == []):
        curr = stack.pop(-1)
        result.append(curr.val)
        if not curr.right == None: stack.append(curr.right)
        if not curr.left == None: stack.append(curr.left)
    return result
```
---
**Recursive version** of Postorder Traversal

```
def preorderTraversal(self, root):
    if root == None: return []
    return self.inorderTraversal(root.left) + self.inorderTraversal(root.right) + root.val
```

**Iterative version** of Postorder Traversal

```
def postorderTraversal(self, root):
    if root == None: return []
    stack = [root]
    result = []
    while not stack == []:
        curr = stack.pop(-1)
        result = [curr.val] + result
        if not curr.left == None: stack.append(curr.left)
        if not curr.right == None: stack.append(curr.right)
    return result
```

---
**Level Order Traversal**

My Solution:

```
def levelOrder(self, root):
    """
    :type root: TreeNode
    :rtype: List[List[int]]
    """
    if root == None: return []
    queue = []
    result = []
    queue.append((root, 0))
    while (not queue == []) :
        (curr, i) = queue[0]
        queue = queue[1:]
        
        if len(result) <= i:
            result.append([curr.val])
        else:
            result[i].append(curr.val)
            
        if (not curr.left == None):
            queue.append((curr.left, i+1))
        if (not curr.right == None):
            queue.append((curr.right, i+1))
    return result
```

A conciser solution from [this post](https://discuss.leetcode.com/topic/26402/5-6-lines-fast-python-solution-48-ms/2).

```
def levelOrder(self, root):
    if not root:
        return []
    ans, level = [], [root]
    while level:
        ans.append([node.val for node in level])
        temp = []
        for node in level:
            temp.extend([node.left, node.right])
        level = [leaf for leaf in temp if leaf]
    return ans
```

Can be further boiled down:

```
def levelOrder(self, root):
    ans, level = [], [root]
    while root and level:
        ans.append([node.val for node in level])            
        level = [kid for n in level for kid in (n.left, n.right) if kid]
    return ans
```

or:

```
def levelOrder(self, root):
    ans, level = [], [root]
    while root and level:
        ans.append([node.val for node in level])
        LRpair = [(node.left, node.right) for node in level]
        level = [leaf for LR in LRpair for leaf in LR if leaf]
    return ans
```