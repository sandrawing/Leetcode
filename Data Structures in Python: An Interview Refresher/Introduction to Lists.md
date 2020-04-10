**List**

The time complexity of each of these operations is the asymptotic average case taken from the Python Wiki page.

https://wiki.python.org/moin/TimeComplexity

The insert() function

Inserts element to the list. Use it like list.insert(index, value). It works in O(n) time.

The remove() function

Removes the given element at a given index. Use it like list.remove(element). It works in O(n) time. 
If the element does not exist, you will get a runtime error.

The pop() function
Removes the element at given index. If no index is given, then it removes the last element. So list.pop() would remove the last element. This works in O(1). list.pop(2) would remove the element with index 2, i.e., 55 in this case. Also, popping the kth intermediate element takes O(k) time where k < n.

list[start:stop:step]

Here step specifies the increment in the list indices and can also be negative.

The del keyword is used to delete elements from a list. 

In the following example, all the elements at even-numbered indices are deleted.

```ruby
List = list(range(10))
print(List)  # 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
del List[::2]
print(List)  # 1, 3, 5, 7, 9
```

Line 3 uses the del function. Here, the empty start and end indices refer to 0 and length of the list by default, whereas 2 is the step size.

We can use negative numbers to begin indexing the list elements from the end.

**Array**

In Python, an array is just an ordered sequence of homogeneous elements. In other words, an array can only hold elements of one datatype. Python arrays are basically just wrappers for C arrays. The type is constrained and specified at the time of creation.

Initializing Arrays

```ruby
import array
newArray = array.array('type', [list])
```

Here type defines the data type of array and list is a python list containing homogenous elements.

```ruby
import array

# type: 'd' (float), initializer list: [1, 2, 3]
newArray = array.array('d', [1, 2, 3])
print(newArray[0])
```

Changing or adding array elements

Arrays are mutable; their elements can be changed in the same way as list elements. Have a look at the following coding widget.

```ruby
import array
integers = array.array('i', [1, 2, 3, 5, 7, 10])

# changing first element
integers[0] = 0
print(integers)  # array('i', [0, 2, 3, 5, 7, 10])

# changing 3rd to 5th element
integers[2:5] = array.array('i', [4, 6, 8])
print(integers)     # Output: array('i', [0, 2, 4, 6, 8, 10])
```

We can use the remove(val) method to remove the given item or pop(index) to remove an item at the given index. The remove(val) method removes the first element that is equal to val in the array.

```ruby
import array

IntegerArray = array.array('i', [10, 11, 12, 12, 13])

IntegerArray.remove(12)
print(IntegerArray)   # array('i', [10, 11, 12, 13])

print(IntegerArray.pop(2))   # Output: 12
print(IntegerArray)   # array('i', [10, 11, 13])
```

**Lists vs Arrays**

Differences #
Python lists are very flexible and can hold completely heterogeneous arbitrary data, but they use a lot more space than Python arrays. Each list contains pointers to a block of pointers, each of which in turn points to a full Python object. Again, the advantage of the list is flexibility: because each list element is a full structure containing both data and type information, the list can be filled with data of any desired type. Arrays lack this flexibility but are much more efficient for storing and manipulating data.

The differences between the two largely exist because of the aforementioned backend implementation. Arrays in Python are implemented just like C arrays, with a pointer pointing to the first element of the array with the rest existing contiguously in the memory.

Similarities

Arrays and lists are very similar in syntactical usage and functionality. Both are used to store data. Both are mutable, i.e., the data in both is not constant and can be modified. Both can also be indexed and iterated through. Both can be sliced and are in fact sliced the same way.

When to use arrays and when to use lists

Because of the way that lists are implemented, elements can be appended to them very efficiently. If you want your collection to grow and shrink in a time-efficient manner, then lists should be used. It’s also better to use lists if you need to manage lots of different data types, however, arrays are better when you need to store a lot of data and perform a large number of computationally intensive mathematical operations. Note that the arrays from the NumPy library of Python are better suited for mathematical use cases.
