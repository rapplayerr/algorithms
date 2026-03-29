# Задача [121]: [best-time-to-buy-and-sell-stock]

**Дата:** 2026-03-29
**Сложность:** Easy
**Паттерн:** sliding window

## Концепция
You are given an array prices where prices[i] is the price of a given stock on the ith day.

You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.


идем по списку вторым указателем и считаем профит или смещаем первый в зависимости от выполнения условия

## Ключевая идея
используем факт невозможности продажи до покупки и применяем скользящее окно как самый рациональный метод.

## Пошаговый разбор
1. создаем левый указатель, он будет отвечать за покупку.
2. запускаем цикл для правого указателя и если видим большее значение - считаем профит. в противном случае (нашли меньшую или равную цену - перемещаем левый указатель на его место)
3. сравниваем текущий профит с максимальным и берем больший, делаем так до конца цикла, возвращаем максимальный профит.

## Моё решение
```python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        left = 0
        max_profit = 0
        
        for right in range(1, len(prices)):
            if prices[right] > prices[left]:
                profit = prices[right] - prices[left]
                max_profit = max(max_profit, profit)
            else:
                left = right
                
        return max_profit