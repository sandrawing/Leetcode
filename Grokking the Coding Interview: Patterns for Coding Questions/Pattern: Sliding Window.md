The efficient way to solve this problem would be to visualize each contiguous subarray as a sliding window of ‘5’ elements. This means that when we move on to the next subarray, we will slide the window by one element. So, to reuse the sum from the previous subarray, we will subtract the element going out of the window and add the element now being included in the sliding window. This will save us from going through the whole subarray to find the sum and, as a result, the algorithm complexity will reduce to O(N).


Problem 1

Given an array of positive numbers and a positive number ‘k’, find the maximum sum of any contiguous subarray of size ‘k’.

1. My solution

```ruby
def max_sub_array_of_size_k(k, arr):
  max_sum = 0
  for i in range(len(arr) - k):
    max_sum = max(max_sum, sum(arr[i:i+k]))
  return max_sum
```

2. Solution

```ruby
def max_sub_array_of_size_k(k, arr):
  max_sum , window_sum = 0, 0
  window_start = 0

  for window_end in range(len(arr)):
    window_sum += arr[window_end]  # add the next element
    # slide the window, we don't need to slide if we've not hit the required window size of 'k'
    if window_end >= k-1:
      max_sum = max(max_sum, window_sum)
      window_sum -= arr[window_start]  # subtract the element going out
      window_start += 1  # slide the window ahead
  return max_sum


def main():
  print("Maximum sum of a subarray of size K: " + str(max_sub_array_of_size_k(3, [2, 1, 5, 1, 3, 2])))
  print("Maximum sum of a subarray of size K: " + str(max_sub_array_of_size_k(2, [2, 3, 4, 1, 5])))

main()
```

Problem 2

Given an array of positive numbers and a positive number ‘S’, find the length of the smallest contiguous subarray whose sum is greater than or equal to ‘S’. Return 0, if no such subarray exists.

1. My Solution

```ruby
def smallest_subarray_with_given_sum(s, arr):
  # TODO: Write your code here
  length = 0
  i, j = 0, 0
  while i < len(arr) and j < len(arr):
    curr_sum = sum(arr[i:j+1])
    if curr_sum >= s:
      # 这个地方写的不是很简洁 因为要求的是minimum的 如果开始设置成0 会导致后面每次更新有点麻烦
      if length != 0:
        length = min(length, j - i + 1)
      else:
        length = j - i + 1
      i += 1
    else:
      j += 1
  return length
  ```
  
2. Solution
  
```ruby
import math


def smallest_subarray_with_given_sum(s, arr):
  window_sum = 0
  min_length = math.inf
  window_start = 0

  for window_end in range(0, len(arr)):
    window_sum += arr[window_end]  # add the next element
    # shrink the window as small as possible until the 'window_sum' is smaller than 's'
    while window_sum >= s:
      min_length = min(min_length, window_end - window_start + 1)
      window_sum -= arr[window_start]
      window_start += 1
  if min_length == math.inf:
    return 0
  return min_length


def main():
  print("Smallest subarray length: " + str(smallest_subarray_with_given_sum(7, [2, 1, 5, 2, 3, 2])))
  print("Smallest subarray length: " + str(smallest_subarray_with_given_sum(7, [2, 1, 5, 2, 8])))
  print("Smallest subarray length: " + str(smallest_subarray_with_given_sum(8, [3, 4, 1, 1, 6])))


main()
```

Time Complexity #

The time complexity of the above algorithm will be O(N). 

The outer for loop runs for all elements and the inner while loop processes each element only once, therefore the time complexity of the algorithm will be O(N+N) which is asymptotically equivalent to O(N).

The ‘while’ loop can iterate a maximum of ‘n’ times, as it is shrinking the sliding window (we can’t have more than ‘n’ executions of windowStart++). This means the overall time complexity will be O(n+n); ‘n’ for the ‘for’ loop and an ‘n’ for the ‘while’ loop. This is asymptotically equivalent to o(n).

Space Complexity #
The algorithm runs in constant space O(1).

Problem 3


