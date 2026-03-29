# Задача [1817]: [finding-the-users-active-minutes]

**Дата:** 2026-03-04
**Сложность:** Medium
**Паттерн:** hash-map + set, freq counting, bucketsort

## Концепция
You are given the logs for users' actions on LeetCode, and an integer k. The logs are represented by a 2D integer array logs where each logs[i] = [IDi, timei] indicates that the user with IDi performed an action at the minute timei.

Multiple users can perform actions simultaneously, and a single user can perform multiple actions in the same minute.

The user active minutes (UAM) for a given user is defined as the number of unique minutes in which the user performed an action on LeetCode. A minute can only be counted once, even if multiple actions occur during it.

You are to calculate a 1-indexed array answer of size k such that, for each j (1 <= j <= k), answer[j] is the number of users whose UAM equals j.

Return the array answer as described above.

сначала создаем словарь с ключами-пользователями и значениями-множествами в которых хранятся минуты соответсвенно этот сет будет составлять UAM конкретного юзера. важно использовать именно сет для мгновенного подсчета длины, а также для избежания дубликатов, так как один и тот же юзер может совершать несколько действий в одну минуту но эта минута не может считаться дважды. затем создаем массив из k нулей и для каждого uam считаем количество юзеров соответствующий этому значению.

## Ключевая идея
использование хеш таблицы вместе с сетом.

## Пошаговый разбор
1. за 1 проход заполняем хеш таблицу.
2. за второй проход по значениям хеш таблицы заполняем результирующий массив.
3. важно помнить что результирующий список начинается с 1.

## Моё решение
```python
from collections import defaultdict

class Solution(object):
    def findingUsersActiveMinutes(self, logs, k):
        """
        :type logs: List[List[int]]
        :type k: int
        :rtype: List[int]
        """
        hm = defaultdict(set)
        res = [0]*k
        for i in logs:
            hm[i[0]].add(i[1])
        for v in hm.values():
            res[len(v)-1]+=1
        return res