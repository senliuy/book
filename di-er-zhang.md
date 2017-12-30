# 121. Best Time to Buy and Sell Stock

直达：https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/

Say you have an array for which theithelement is the price of a given stock on dayi.

If you were only permitted to complete at most one transaction \(ie, buy one and sell one share of the stock\), design an algorithm to find the maximum profit.

**Example 1:**

```
Input: [7, 1, 5, 3, 6, 4]
Output: 5

max. difference = 6-1 = 5 (not 7-1 = 6, as selling price needs to be larger than buying price)
```

**Example 2:**

```
Input: [7, 6, 4, 3, 1]
Output: 0

In this case, no transaction is done, i.e. max profit = 0.
```

## 分析

保存两个变量

1. minPrice：当前遍历到的最少买入价格；
2. maxProfit: 最大收益；

则更新公式为：

1. minPrice = min\(prices\[i\], minPrice\);
2. maxProfit = max\(maxProfit, prices\[i\]-minPrice\);

## C++代码

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        if(prices.size() <= 0) return 0;
        int minPrice = prices[0];
        int maxProfit = 0;
        for(int i=0; i< prices.size(); i++){
            minPrice = min(prices[i], minPrice);
            maxProfit = max(maxProfit, prices[i] - minPrice);
        }
        return maxProfit;
    }
};
```

## Python代码

```py
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        res = 0
        if (len(prices) <= 1):
            return 0
        minPrice = prices[0]
        maxProfit = 0
        for price in prices:
            minPrice = min(minPrice, price)
            maxProfit = max(maxProfit, price-minPrice)
        return maxProfit
        
```



