# Задача [15]: [3-sum]

**Дата:** 06-03-2026
**Сложность:** Medium
**Паттерн:** two-pointers

## Концепция
Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

Notice that the solution set must not contain duplicate triplets.


сортируем массив, используем три указателя. первый - фиксирующий, два других - поисковые. фиксирующий указатель устанавливается в начало списка, а оставшаяся его часть проверяется на наличие таких двух элементов, что их сумма равна отрицательному фиксированному элементу (чтобы получить ноль). 

## Ключевая идея
понять, что если отсортировать массив, то решение сводится к обычной задаче с двумя указателями (в нашем случае с тремя).

## Пошаговый разбор
1. сортируем список.
2. запускаем цикл для slow указателя, заодно проверяем на дубликаты, чтобы не вернуть повторяющиеся пары и в целом оптимизировать решение.
3. также делаем и для поисковых указателей, двигаем их в зависимости от величины их суммы, пропуская при это дубликаты.

## Моё решение
```python
class Solution(object):
    def threeSum(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        if len(nums) < 3:
            return []
        n=len(nums)
        snums = sorted(nums)
        res = []
        for slow in range(n-2):
            if slow > 0 and snums[slow] == snums[slow-1]:
                continue
            left = slow + 1
            right = n-1
            while left < right:
                if snums[left] + snums[right] > -snums[slow]:
                    right -= 1
                elif snums[left] + snums[right] < -snums[slow]:
                    left += 1
                else:                        
                    res.append(list((snums[slow], snums[left], snums[right])))
                    while left < right and snums[left] == snums[left+1]:
                        left+=1
                    while left < right and snums[right] == snums[right-1]:
                        right-=1
                    left+=1
                    right-=1
        return res