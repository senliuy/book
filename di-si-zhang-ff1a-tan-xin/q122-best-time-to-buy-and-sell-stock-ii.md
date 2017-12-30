# 122. Best Time to Buy and Sell Stock II

直达：[https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/description/](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/description/)

Say you have an array for which the $$i^{th}$$ element is the price of a given stock on day $$i$$.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like \(ie, buy one and sell one share of the stock multiple times\). However, you may not engage in multiple transactions at the same time \(ie, you must sell the stock before you buy again\).

## 分析

只要这一天比前一天股票价格高，就会有收入，因此可以使用贪心算法。

## C++代码

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int res = 0;
        if(prices.size() > 0) int minPrice = prices[0];
        for(int i = 1; i<prices.size(); i++){
            if(prices[i] - prices[i-1] > 0) res += prices[i] - prices[i-1];
        }
        return res;
    }
};
```



