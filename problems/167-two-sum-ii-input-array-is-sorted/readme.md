# Задача [167]: [two-sum-ii-input-array-is-sorted]

**Дата:** 06-03-2026
**Сложность:** Medium
**Паттерн:** two-pointers

## Концепция
Given a 1-indexed array of integers numbers that is already sorted in non-decreasing order, find two numbers such that they add up to a specific target number. Let these two numbers be numbers[index1] and numbers[index2] where 1 <= index1 < index2 <= numbers.length.

Return the indices of the two numbers index1 and index2, each incremented by one, as an integer array [index1, index2] of length 2.

The tests are generated such that there is exactly one solution. You may not use the same element twice.

Your solution must use only constant extra space.


проходим по списку с двух концов, сначала проверяем на равнество с target, если равно - сразу возвращаем пару, если больше - двигаем левый указатель, так как список отсортирован, если меньше - правый соответственно.

## Ключевая идея
отсортированный список - сильный намек на использование двух указателей.

## Пошаговый разбор
1. объявляем указатели, левый 0, правый n-1.
2. пока левый меньше правого: выполняем условия.
3. результат можно возвращать сразу, так как в массиве только одна пара удовлетворяющая условию.

## Моё решение
```python
class Solution(object):
    def twoSum(self, numbers, target):
        """
        :type numbers: List[int]
        :type target: int
        :rtype: List[int]
        """
        left = 0
        right = len(numbers) - 1
        while left < right:
            if numbers[left] + numbers[right] == target:
                return [left+1,right+1]
            elif numbers[left] + numbers[right] > target:
                right -= 1
            elif numbers[left] + numbers[right] < target:
                left += 1
        return []