# Задача [0350]: [intersection-of-two-arrays]

**Дата:** 2026-03-03
**Сложность:** Easy
**Паттерн:** хеш-таблица, подсчет частоты

## Концепция
Given two integer arrays nums1 and nums2, return an array of their intersection. Each element in the result must appear as many times as it shows in both arrays and you may return the result in any order.

задача требует хеширования элементов одного из массивов с указанием их частоты в массиве, затем, при проходе по второму массиву, находим пересечения массивов и уменьшаем частоту втретившегося элемента.

## Ключевая идея
{элемент: сколько раз встретился}

## Пошаговый разбор
1. проходим по первому массиву и заполняем хеш таблицу.
2. проходим по второму массиву, сверяем каждый элемент с хеш таблицей: если элемент есть и его частота > 0, записываем в результирующий список, уменьшаем частоту на 1.
3. возвращаем результат.

## Моё решение
```python
class Solution(object):
    def intersect(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: List[int]
        """
        hm={}
        res = []
        for i in nums1:
            hm[i] = hm.get(i,0)+1
        for i in nums2:
            if i in hm and hm[i]>0:
                hm[i]-=1
                res.append(i)
        return res