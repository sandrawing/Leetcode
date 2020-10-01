https://www.hackerrank.com/challenges/max-array-sum/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=dynamic-programming

Given an array of integers, find the subset of non-adjacent elements with the maximum sum. Calculate the sum of that subset.

My previous answer (exceed time limit)

```ruby
def maxSubsetSum(arr):
    dp_curr = [arr[0], arr[1]]
    for i in range(2, len(arr)):
        if max(dp_curr[:i-1]) > 0:
            dp_curr.append(arr[i] + max(dp_curr[:i-1]))
        else:
            dp_curr.append(arr[i])
    return max(dp_curr)
```


```ruby
def maxSubsetSum(arr):
    dp = {} # key : max index of subarray, value = sum
    dp[0], dp[1] = arr[0], max(arr[0], arr[1])
    for i, num in enumerate(arr[2:], start=2):
        dp[i] = max(dp[i-1], dp[i-2]+num, dp[i-2], num)
    return dp[len(arr)-1]
```
