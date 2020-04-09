The time complexity of each of these operations is the asymptotic average case taken from the Python Wiki page.

https://wiki.python.org/moin/TimeComplexity

The insert() function

Inserts element to the list. Use it like list.insert(index, value). It works in O(n) time.

The remove() function

Removes the given element at a given index. Use it like list.remove(element). It works in O(n) time. 
If the element does not exist, you will get a runtime error.

The pop() function
Removes the element at given index. If no index is given, then it removes the last element. So list.pop() would remove the last element. This works in O(1). list.pop(2) would remove the element with index 2, i.e., 55 in this case. Also, popping the kth intermediate element takes O(k) time where k < nk<n.

