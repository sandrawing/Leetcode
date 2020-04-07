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

Leetcode 340

Problem 4

Leetcode 159

My solution 

```ruby
def fruits_into_baskets(fruits):
  # TODO: Write your code here
  if len(fruits) < 3:
    return len(fruits)
  index_dict = {fruits[0]: 0}
  max_len = 1
  start = 0
  for end in range(len(fruits)):
    index_dict[fruits[end]] = end
    if len(index_dict) > 2:
      del_idx = min(index_dict.values())
      del index_dict[fruits[del_idx]]
      start = del_idx + 1
    max_len = max(max_len, end - start + 1)
  return max_len
 ```

Problem 5

Leetcode 3

Problem 6

Leetcode 424

Problem 7

Longest Subarray with Ones after Replacement (hard)

Given an array containing 0s and 1s, if you are allowed to replace no more than ‘k’ 0s with 1s, find the length of the longest contiguous subarray having all 1s.

My solution

```ruby
def length_of_longest_substring(arr, k):
  # TODO: Write your code here
  start = 0
  count = {}
  result = 0
  for end in range(len(arr)):
    if arr[end] in count:
      count[arr[end]] += 1
    else:
      count[arr[end]] = 1
    sum_len = sum(count.values())
    if sum_len <= count.get(1, 0) + k:
      result = max(result, sum_len)
    else:
      count[arr[start]] -= 1
      start += 1
  return result
```

Solution from Educative.io

This problem follows the Sliding Window pattern and is quite similar to Longest Substring with same Letters after Replacement. The only difference is that, in the problem, we only have two characters (1s and 0s) in the input arrays.

Following a similar approach, we’ll iterate through the array to add one number at a time in the window. We’ll also keep track of the maximum number of repeating 1s in the current window (let’s call it maxOnesCount). So at any time, we know that we can have a window which has 1s repeating maxOnesCount time, so we should try to replace the remaining 0s. If we have more than ‘k’ remaining 0s, we should shrink the window as we are not allowed to replace more than ‘k’ 0s.

```ruby
def length_of_longest_substring(arr, k):
  window_start, max_length, max_ones_count = 0, 0, 0

  # Try to extend the range [window_start, window_end]
  for window_end in range(len(arr)):
    if arr[window_end] == 1:
      max_ones_count += 1

    # Current window size is from window_start to window_end, overall we have a maximum of 1s
    # repeating 'max_ones_count' times, this means we can have a window with 'max_ones_count' 1s
    # and the remaining are 0s which should replace with 1s.
    # now, if the remaining 1s are more than 'k', it is the time to shrink the window as we
    # are not allowed to replace more than 'k' 0s
    if (window_end - window_start + 1 - max_ones_count) > k:
      if arr[window_start] == 1:
        max_ones_count -= 1
      window_start += 1

    max_length = max(max_length, window_end - window_start + 1)
  return max_length


def main():
  print(length_of_longest_substring([0, 1, 1, 0, 0, 0, 1, 1, 0, 1, 1], 2))
  print(length_of_longest_substring(
    [0, 1, 0, 0, 1, 1, 0, 1, 1, 0, 0, 1, 1], 3))


main()
```

Time Complexity #
The time complexity of the above algorithm will be O(N) where ‘N’ is the count of numbers in the input array.

Space Complexity #
The algorithm runs in constant space O(1).


Problem Challenge 1

Leetcode 567

Problem Challenge 2

Very similar to Leetcode 567

String Anagrams (hard) #
Given a string and a pattern, find all anagrams of the pattern in the given string.

Anagram is actually a Permutation of a string. For example, “abc” has the following six anagrams:
abc
acb
bac
bca
cab
cba

Write a function to return a list of starting indices of the anagrams of the pattern in the given string.

My solution

```ruby
def find_string_anagrams(str, pattern):
  result_indexes = []
  # TODO: Write your code here
  window_start, matched = 0, 0
  char_frequency = {}

  for chr in pattern:
    if chr not in char_frequency:
      char_frequency[chr] = 0
    char_frequency[chr] += 1

  # our goal is to match all the characters from the 'char_frequency' with the current window
  # try to extend the range [window_start, window_end]
  for window_end in range(len(str)):
    right_char = str[window_end]
    if right_char in char_frequency:
      # decrement the frequency of matched character
      char_frequency[right_char] -= 1
      if char_frequency[right_char] == 0:
        matched += 1

    if matched == len(char_frequency):
      result_indexes.append(window_start)

    # shrink the window by one character
    if window_end >= len(pattern) - 1:
      left_char = str[window_start]
      window_start += 1
      if left_char in char_frequency:
        if char_frequency[left_char] == 0:
          matched -= 1
        char_frequency[left_char] += 1
  return result_indexes
```

Solution from Educative.io

```ruby
def find_string_anagrams(str, pattern):
  window_start, matched = 0, 0
  char_frequency = {}

  for chr in pattern:
    if chr not in char_frequency:
      char_frequency[chr] = 0
    char_frequency[chr] += 1

  result_indices = []
  # Our goal is to match all the characters from the 'char_frequency' with the current window
  # try to extend the range [window_start, window_end]
  for window_end in range(len(str)):
    right_char = str[window_end]
    if right_char in char_frequency:
      # Decrement the frequency of matched character
      char_frequency[right_char] -= 1
      if char_frequency[right_char] == 0:
        matched += 1

    if matched == len(char_frequency):  # Have we found an anagram?
      result_indices.append(window_start)

    # Shrink the sliding window
    if window_end >= len(pattern) - 1:
      left_char = str[window_start]
      window_start += 1
      if left_char in char_frequency:
        if char_frequency[left_char] == 0:
          matched -= 1  # Before putting the character back, decrement the matched count
        char_frequency[left_char] += 1  # Put the character back

  return result_indices


def main():
  print(find_string_anagrams("ppqp", "pq"))
  print(find_string_anagrams("abbcabc", "abc"))


main()
```
