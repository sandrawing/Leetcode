Given an array of sorted numbers and a target sum, find a pair in the array whose sum is equal to the given target.

Given that the input array is sorted, an efficient way would be to start with one pointer in the beginning and another pointer at the end. At every step, we will see if the numbers pointed by the two pointers add up to the target sum. If they do not, we will do one of two things:

If the sum of the two numbers pointed by the two pointers is greater than the target sum, this means that we need a pair with a smaller sum. So, to try more pairs, we can decrement the end-pointer.

If the sum of the two numbers pointed by the two pointers is smaller than the target sum, this means that we need a pair with a larger sum. So, to try more pairs, we can increment the start-pointer.

The time complexity of the above algorithm will be O(N).

Problem 1

Given an array of sorted numbers and a target sum, find a pair in the array whose sum is equal to the given target.

Write a function to return the indices of the two numbers (i.e. the pair) such that they add up to the given target.

My answer

```ruby
def pair_with_targetsum(arr, target_sum):
  # TODO: Write your code here
  p_start = 0
  p_end = len(arr) - 1
  while p_start != p_end:
    if arr[p_end] + arr[p_start] == target_sum:
      return [p_start, p_end]
    elif arr[p_end] + arr[p_start] < target_sum:
      p_start += 1
    else:
      p_end -= 1
  return [-1, -1]
```

Answer from Educative.io

```ruby
def pair_with_targetsum(arr, target_sum):
  left, right = 0, len(arr) - 1
  while(left < right):
    current_sum = arr[left] + arr[right]
    if current_sum == target_sum:
      return [left, right]

    if target_sum > current_sum:
      left += 1  # we need a pair with a bigger sum
    else:
      right -= 1  # we need a pair with a smaller sum
  return [-1, -1]


def main():
  print(pair_with_targetsum([1, 2, 3, 4, 6], 6))
  print(pair_with_targetsum([2, 5, 9, 11], 11))


main()
```

Time Complexity #
The time complexity of the above algorithm will be O(N), where ‘N’ is the total number of elements in the given array.

Space Complexity #
The algorithm runs in constant space O(1).

Alternative Solution: Hash Table

Instead of using a two-pointer or a binary search approach, we can utilize a HashTable to search for the required pair. We can iterate through the array one number at a time. Let’s say during our iteration we are at number ‘X’, so we need to find ‘Y’ such that “X + Y == Target”. We will do two things here:

Search for ‘Y’ (which is equivalent to “Target - X”) in the HashTable. If it is there, we have found the required pair.
Otherwise, insert “X” in the HashTable, so that we can search it for the later numbers.

```ruby
def pair_with_targetsum(arr, target_sum):
  nums = {}  # to store numbers and their indices
  for i, num in enumerate(arr):
    if target_sum - num in nums:
      return [nums[target_sum - num], i]
    else:
      nums[arr[i]] = i
  return [-1, -1]


def main():
  print(pair_with_targetsum([1, 2, 3, 4, 6], 6))
  print(pair_with_targetsum([2, 5, 9, 11], 11))


main()
```
Time Complexity #
The time complexity of the above algorithm will be O(N), where ‘N’ is the total number of elements in the given array.

Space Complexity #
The space complexity will also be O(N), as, in the worst case, we will be pushing ‘N’ numbers in the HashTable.


Problem 3

Given a sorted array, create a new array containing squares of all the number of the input array in the sorted order.

```ruby
def make_squares(arr):
  n = len(arr)
  squares = [0 for x in range(n)]
  highestSquareIdx = n - 1
  left, right = 0, n - 1
  while left <= right:
    leftSquare = arr[left] * arr[left]
    rightSquare = arr[right] * arr[right]
    if leftSquare > rightSquare:
      squares[highestSquareIdx] = leftSquare
      left += 1
    else:
      squares[highestSquareIdx] = rightSquare
      right -= 1
    highestSquareIdx -= 1

  return squares


def main():

  print("Squares: " + str(make_squares([-2, -1, 0, 2, 3])))
  print("Squares: " + str(make_squares([-3, -1, 0, 1, 2])))


main()
```

Problem Challenge 3

Minimum Window Sort (medium) #
Given an array, find the length of the smallest subarray in it which when sorted will sort the whole array.

Solution #
As we know, once an array is sorted (in ascending order), the smallest number is at the beginning and the largest number is at the end of the array. So if we start from the beginning of the array to find the first element which is out of sorting order i.e., which is smaller than its previous element, and similarly from the end of array to find the first element which is bigger than its previous element, will sorting the subarray between these two numbers result in the whole array being sorted?

Let’s try to understand this with Example-2 mentioned above. In the following array, what are the first numbers out of sorting order from the beginning and the end of the array:

    [1, 3, 2, 0, -1, 7, 10]
    
Starting from the beginning of the array the first number out of the sorting order is ‘2’ as it is smaller than its previous element which is ‘3’.
Starting from the end of the array the first number out of the sorting order is ‘0’ as it is bigger than its previous element which is ‘-1’
As you can see, sorting the numbers between ‘3’ and ‘-1’ will not sort the whole array. To see this, the following will be our original array after the sorted subarray:

    [1, -1, 0, 2, 3, 7, 10]
    
The problem here is that the smallest number of our subarray is ‘-1’ which dictates that we need to include more numbers from the beginning of the array to make the whole array sorted. We will have a similar problem if the maximum of the subarray is bigger than some elements at the end of the array. To sort the whole array we need to include all such elements that are smaller than the biggest element of the subarray. So our final algorithm will look like:

From the beginning and end of the array, find the first elements that are out of the sorting order. The two elements will be our candidate subarray.

Find the maximum and minimum of this subarray.

Extend the subarray from beginning to include any number which is bigger than the minimum of the subarray.

Similarly, extend the subarray from the end to include any number which is smaller than the maximum of the subarray.

```ruby
import math


def shortest_window_sort(arr):
  low, high = 0, len(arr) - 1
  # find the first number out of sorting order from the beginning
  while (low < len(arr) - 1 and arr[low] <= arr[low + 1]):
    low += 1

  if low == len(arr) - 1:  # if the array is sorted
    return 0

  # find the first number out of sorting order from the end
  while (high > 0 and arr[high] >= arr[high - 1]):
    high -= 1

  # find the maximum and minimum of the subarray
  subarray_max = -math.inf
  subarray_min = math.inf
  for k in range(low, high+1):
    subarray_max = max(subarray_max, arr[k])
    subarray_min = min(subarray_min, arr[k])

  # extend the subarray to include any number which is bigger than the minimum of the subarray
  while (low > 0 and arr[low-1] > subarray_min):
    low -= 1
  # extend the subarray to include any number which is smaller than the maximum of the subarray
  while (high < len(arr)-1 and arr[high+1] < subarray_max):
    high += 1

  return high - low + 1


def main():
  print(shortest_window_sort([1, 2, 5, 3, 7, 10, 9, 12]))
  print(shortest_window_sort([1, 3, 2, 0, -1, 7, 10]))
  print(shortest_window_sort([1, 2, 3]))
  print(shortest_window_sort([3, 2, 1]))


main()
```

Time complexity #
The time complexity of the above algorithm will be O(N).

Space complexity #
The algorithm runs in constant space O(1).
