# Задача [74]: [search-a-2d-matrix]

**Дата:** 2026-03-29
**Сложность:** Medium
**Паттерн:** binary search

## Концепция
You are given an m x n integer matrix matrix with the following two properties:

Each row is sorted in non-decreasing order.
The first integer of each row is greater than the last integer of the previous row.
Given an integer target, return true if target is in matrix or false otherwise.

You must write a solution in O(log(m * n)) time complexity.


ищем сначала нужную строку, с помощью бинарного поиска, затем так же бинарным поиском ищем цель в строке.

## Ключевая идея
матрица отсортирована построчно, значит ее можно представить в виде обычного отсортированного списка, где бинарный поиск - стандартный прием.

## Пошаговый разбор
1. сначала ищем строку для которой выполняются два условия: первый элемент меньше цели, последний - больше. если такой строки нет: возвращаем фолс
2. если нашли строку: повторяем поиск.
3. возвращаем значение в зависимости от выполненного условия о равности.

## Моё решение
```python
class Solution(object):
    def searchMatrix(self, matrix, target):
        """
        :type matrix: List[List[int]]
        :type target: int
        :rtype: bool
        """
        left = 0 
        right = len(matrix) - 1
        while left <= right:
            mid = (left + right) // 2
            if matrix[mid][0] > target:
                right = mid - 1
            elif matrix[mid][-1] < target:
                left = mid + 1
            else:
                left1 = 0
                right1 = len(matrix[mid]) - 1
                while left1 <= right1:
                    mid1 = (left1 + right1) // 2
                    if matrix[mid][mid1] == target:
                        return True
                    elif matrix[mid][mid1] > target:
                        right1 = mid1 - 1
                    elif matrix[mid][mid1] < target:
                        left1 = mid1 + 1
                return False
        return False