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

Insertion in a Max-Heap

Here is a high-level description of the algorithm to insert elements into a heap and maintain the heap property.

Create a new child node at the end of the heap

Place the new key at that node

Then, restore the heap property by swapping parent and child values if the parent key is smaller than the child key. We call this ‘percolating up’.

Continue to percolate up until the heap property is restored.

Remove Maximum in a Max Heap

Delete the root node

Move the key of last child node at last level to the root

Now compare the key with its children and if the key is smaller than the key at any of the child nodes, swap values. We call this ‘max heapifying.’

Continue to max heapify until the heap property is restored.

Implementation of MaxHeap

```ruby
class MaxHeap:
    def __init__(self):
        self.heap = []

    def insert(self, val):
        self.heap.append(val)
        self.__percolateUp(len(self.heap)-1)

    def getMax(self):
        if self.heap:
            return self.heap[0]
        return None

    def removeMax(self):
        if len(self.heap) > 1:
            max = self.heap[0]
            self.heap[0] = self.heap[-1]
            del self.heap[-1]
            self.__maxHeapify(0)
            return max
        elif len(self.heap) == 1:
            max = self.heap[0]
            del self.heap[0]
            return max
        else:
            return None

    def __percolateUp(self, index):
        parent = (index-1)//2
        if index <= 0:
            return
        elif self.heap[parent] < self.heap[index]:
            tmp = self.heap[parent]
            self.heap[parent] = self.heap[index]
            self.heap[index] = tmp
            self.__percolateUp(parent)

    def __maxHeapify(self, index):
        left = (index * 2) + 1
        right = (index * 2) + 2
        largest = index
        if len(self.heap) > left and self.heap[largest] < self.heap[left]:
            largest = left
        if len(self.heap) > right and self.heap[largest] < self.heap[right]:
            largest = right
        if largest != index:
            tmp = self.heap[largest]
            self.heap[largest] = self.heap[index]
            self.heap[index] = tmp
            self.__maxHeapify(largest)

    def buildHeap(self, arr):
        self.heap = arr
        for i in range(len(arr)-1, -1, -1):
            self.__maxHeapify(i)


heap = MaxHeap()
heap.insert(12)
heap.insert(10)
heap.insert(-10)
heap.insert(100)

print(heap.getMax())
```
