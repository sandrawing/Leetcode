```ruby
public static double maxDrawdown(double[] prices) {
  if (prices.length <= 1) return 0;

  double maxPrice = prices[0];
  double maxDd = 0;

  for (int i = 1; i < prices.length; i++) {
    if (prices[i] > maxPrice) maxPrice = prices[i];
    else if (prices[i] < maxPrice) maxDd = Math.min(maxDd, prices[i] / maxPrice - 1);
  }

  return maxDd;
}
```
