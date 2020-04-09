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
