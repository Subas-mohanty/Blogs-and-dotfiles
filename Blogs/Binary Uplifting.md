### What is binary uplifting ?
Binary lifting (also known as binary jumping) is a dynamic programming technique used to efficiently answer queries on tree structures, such as finding the Lowest Common Ancestor (LCA) or the k-th ancestor of a node. 

### How does it do this ?
So it maintains a `up` or `parent` or `ancestors` array which is a 2D array where up(node)(j) represents the 2^jth ancestor of the node.

### But why representing in 2's power/exponent ?
Because every number can be represented in unique power of 2
for e.g. 14 = 1110 => 2^3 + 2^2 + 2^1 

### How to find it ?
To find the jth ancestor of a node we can write a recurrence relation as
2^j = 2^j-1 + 2^j-1
because 2 * 2^j-1 = 2^j

so the recurrence becomes 
```
parent[node][j] = parent[parent[node][j-1]][j-1]
// finding the j-1th ancestor(2^j-1th) and that nodes 2^j-1th ancestor
```
