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

Build heap from Array

Simple Approach: Suppose, we need to build a Max-Heap from the above-given array elements. It can be clearly seen that the above complete binary tree formed does not follow the Heap property. So, the idea is to heapify the complete binary tree formed from the array in reverse level order following a top-down approach.

That is first heapify, the last node in level order traversal of the tree, then heapify the second last node and so on.

Time Complexity: Heapify a single node takes O(log N) time complexity where N is the total number of Nodes. Therefore, building the entire Heap will take N heapify operations and the total time complexity will be O(N*logN).

In reality, building a heap takes O(n) time depending on the implementation which can be seen here.

Optimized Approach: The above approach can be optimized by observing the fact that the leaf nodes need not to be heapified as they already follow the heap property. Also, the array representation of the complete binary tree contains the level order traversal of the tree.

```ruby
# Python3 program for building Heap from Array 
  
# To heapify a subtree rooted with node i  
# which is an index in arr[]. N is size of heap 
def heapify(arr, n, i): 
  
    largest = i; # Initialize largest as root 
    l = 2 * i + 1; # left = 2*i + 1 
    r = 2 * i + 2; # right = 2*i + 2 
  
    # If left child is larger than root 
    if l < n and arr[l] > arr[largest]: 
        largest = l; 
  
    # If right child is larger than largest so far 
    if r < n and arr[r] > arr[largest]: 
        largest = r; 
  
    # If largest is not root 
    if largest != i: 
        arr[i], arr[largest] = arr[largest], arr[i]; 
  
        # Recursively heapify the affected sub-tree 
        heapify(arr, n, largest); 
  
# Function to build a Max-Heap from the given array 
def buildHeap(arr, n): 
  
    # Index of last non-leaf node 
    startIdx = n // 2 - 1; 
  
    # Perform reverse level order traversal 
    # from last non-leaf node and heapify 
    # each node 
    for i in range(startIdx, -1, -1): 
        heapify(arr, n, i); 
  
# A utility function to print the array 
# representation of Heap 
def printHeap(arr, n): 
    print("Array representation of Heap is:"); 
  
    for i in range(n): 
        print(arr[i], end = " "); 
    print(); 
```

Min-heap Implementation

```ruby
class MinHeap:
    def __init__(self):
        self.heap = []

    def insert(self, val):
        self.heap.append(val)
        self.__percolateUp(len(self.heap)-1)

    def getMin(self):
        if self.heap:
            return self.heap[0]
        return None

    def removeMin(self):
        if len(self.heap) > 1:
            min = self.heap[0]
            self.heap[0] = self.heap[-1]
            del self.heap[-1]
            self.__minHeapify(0)
            return min
        elif len(self.heap == 1):
            min = self.heap[0]
            del self.heap[0]
            return min
        else:
            return None

    def __percolateUp(self, index):
        parent = (index-1)//2
        if index <= 0:
            return
        elif self.heap[parent] > self.heap[index]:
            tmp = self.heap[parent]
            self.heap[parent] = self.heap[index]
            self.heap[index] = tmp
            self.__percolateUp(parent)

    def __minHeapify(self, index):
        left = (index * 2) + 1
        right = (index * 2) + 2
        smallest = index
        if len(self.heap) > left and self.heap[smallest] > self.heap[left]:
            smallest = left
        if len(self.heap) > right and self.heap[smallest] > self.heap[right]:
            smallest = right
        if smallest != index:
            tmp = self.heap[smallest]
            self.heap[smallest] = self.heap[index]
            self.heap[index] = tmp
            self.__minHeapify(smallest)

    def buildHeap(self, arr):
        self.heap = arr
        for i in range(len(arr)-1, -1, -1):
            self.__minHeapify(i)


heap = MinHeap()
heap.insert(12)
heap.insert(10)
heap.insert(-10)
heap.insert(100)

print(heap.getMin())
print(heap.removeMin())
print(heap.getMin())
heap.insert(-100)
print(heap.getMin())
```

Convert max-heap to min-heap

```ruby
def minHeapify(heap, index):
    left = index * 2 + 1
    right = (index * 2) + 2
    smallest = index
    # check if left child exists and is less than smallest
    if len(heap) > left and heap[smallest] > heap[left]:
        smallest = left
    # check if right child exists and is less than smallest
    if len(heap) > right and heap[smallest] > heap[right]:
        smallest = right
    # check if current index is not the smallest
    if smallest != index:
        # swap current index value with smallest
        tmp = heap[smallest]
        heap[smallest] = heap[index]
        heap[index] = tmp
        # minHeapify the new node
        minHeapify(heap, smallest)
    return heap


def convertMax(maxHeap):
    # iterate from middle to first element
    # middle to first indices contain all parent nodes
    for i in range((len(maxHeap))//2, -1, -1):
        # call minHeapify on all parent nodes
        maxHeap = minHeapify(maxHeap, i)
    return maxHeap


maxHeap = [9, 4, 7, 1, -2, 6, 5]
print(convertMax(maxHeap))
```
