---
title: "Linear Algebra in Python"
permalink: /blog/python_02/
date: 2021-01-02 11:43
background:

categories:
  - blog
tags:
  - blog
  - python
last_modified_at: 2021-01-02T12:01:19+09:00
---

studied with the lecture below: 

[머신러닝을 위한 파이썬](https://www.boostcourse.org/ai222/lecture/24523)

---

I have used MATLAB for linear algebra, but I need to be able to do some of the tasks on `Python` as well. The order of row and column is a bit confusing but will be used to it soon with practice.

# Vector Calculation

```python
u = [2,2]
v = [2,3]
z = [3,5]

list(zip(u,v,z))
# [(2,2,3),(2,3,5)]
[sum(t) for t in zip(u,v,z)]
# [7,10]
```

# Matrix

## Sum

```python
# A =「3 6        B =「5 8
#      4 5」           6 7」

matrix_a = [[3,6],[4,5]]
matrix_b = [[5,8],[6,7]]
result = [[sum(row) for row in zip(*t)] for t in zip(matrix_a, matrix_b)]
# zip(matrix_a, matrix_b) :
# [([3,6], [5,8]), <--t[0]
#  ([4,5], [6,7])] <--t[1]

# w/o unpacking
# zip(t[0]) : [([3,6], ), ([5,8], )]
# zip(t[1]) : [([4,5], ), ([6,7], )]

# w/ unpacking
# zip(*t[0]) : [(3,5), (6,8)]  <-- row 1
# zip(*t[1]) : [(4,6), (5,7)]  <-- row 2

# result: [[8,14],[10,12]]
```

## Transpose

```python
matrix_a = [[1,2,3], [4,5,6]]
result = [[element for element in t] for t in zip(*matrix_a)]
# zip(*matrix_a) :
# [(1,4),(2,5),(3,6)]
# result : 
# [[1,4],[2,5],[3,6]]
```

## Product

```python
# row of matrix : 
# [row for row in matrix]
# column of matrix :
# [col for col in zip(*matrix)]
```

```python
matrix_a = [[1,1,2], [2,1,1]]
matrix_b = [[1,1], [2,1], [1,3]]
result = [[sum(a*b for a,b in zip(row_a, column_b)) \
						for column_b in zip(*matrix_b)] for row_a in matrix_a]
# result : [[5,8], [5,6]]
```