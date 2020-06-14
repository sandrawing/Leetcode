Heaps must be Complete Binary Trees #
As discussed in the chapter on trees, a Complete Binary tree is a tree where each node has at most two children and the nodes at all levels are full, except for the leaf nodes which can be empty.

Some Complete Binary Tree Properties:

All leaves are either at depth dd or depth d-1.
The leaves at depth dd are to the left of the leaves at depth d-1
There is at most one node with just one child
If the singular child exists, it is the left child of its parent
If the singular child exists, it is the right most leaf at depth d.

Min Heaps are built based upon the Min Heap property and Max Heaps are built based upon Max Heap Property. Let’s see how they are different.

Max Heap Property: #
All the parent node keys must be greater than or equal to their child node keys in max-heaps. So the root node will always contain the largest element in the Heap. If Node A has a child node B, then,

key(A) >= key(B)

Min Heap Property: #
In Min-Heaps, all the parent node keys are less than or equal to their child node keys. So the root node, in this case, will always contain the smallest element present in the Heap. If Node A has a child node B, then:

key(A) <= key(B)
