---
title: DFS/BFS
categories: algorithm
tags:
- DFS
- BFS
---


DFS (Depth First Search)
: Recursive / iteration w/ stack

pop last one from stack
and add child node
using stack last pop logic -> retrieve child nodes of last item -> so depth first then retrieve next opposite node of root
 
ex)   1
     / \
    2   5
   / \ / \
  3  4 6  7
stack : 1 -> 2 5 -> 2 6 7 -> 2 6 -> 2 -> 3 4 -> 3 -> end




```java
Stack<T> stack=new Stack();
stack.push(root);
while (!stack.isEmpty()) {
  node=stack.pop();
  if (node.left==null && node.right==null)
    // leaf node to do something
  stack.push(node.left);
  stack.push(node.right);
}
```

BFS (Breath First Search)
: iteration w/ queue


