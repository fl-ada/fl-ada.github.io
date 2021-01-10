---
title: "Pythonic Code"
permalink: /blog/python_01/
date: 2021-01-01 15:25
background:

categories:
  - blog
tags:
  - blog
  - python
last_modified_at: 2021-01-01T15:18:26+09:00
---

studied with the lecture below: [머신러닝을 위한 파이썬](https://www.boostcourse.org/ai222/lecture/24523)

---

My first computer language was `C++`, and jumped into `Python`  to do data analysis. So, yes I used some very pythonic codes, but usually not understanding what it is really. This opportunity allows me to review from the very bottom.

# List Comprehension

For loop in one line, or `[[this]]`, etc. are list comprehension, which is used very often in early stage of data preprocessing.

```python
[i for i in range(10) if i%3==0]
# i : elements of the list
# for i in range(10) : condition 1
# if i%3==0 : condition 2, filter
```

## 1D vs 2D list

### Double for loop, 1D

```python
[i+j for i in word_1 for j in word_2]
# equivalent to
for i in word_1:
	for j in word_2:
		# i+j in list, in 1D
```

### List Comprehension

```python
[[i+j for i in word_1] for j in word_2]
'''
[[word_1[0]+word_2[0], word_1[1]+word_2[0]], # first row
 [word_1[0]+word_2[1], word_1[1]+word_2[1]], # second row
 ...
] # 2D
'''
```

# Zip

Extract values with same index

```python
a,b,c = zip((1,2,3),(10,20,30),(100,200,300))
# a = (1,10,100)
# b = (2,20,200)
# c = (3,30,300)
[sum(x) for x in zip((1,2,3),(10,20,30),(100,200,300))]
# [111,222,333]
```

# Enumerate

Returns (index, value)

```python
alist = ['a1','a2','a3']
blist = ['b1','b2','b3']

for i, (a,b) in enumerate(zip(alist,blist)):
	print(i,a,b)
'''
0 a1 b1
1 a2 b2
2 a3 b3
'''
```

# Lambda

function without definition

```python
f = lambda input1,input2 : output
# equivalent to
def f(input1,input2):
	return output
```

```python
print((lambda x: x+1)(5))
# returns 6 (put x = 5)
```

# Map

run functions to each sequence data

In `python 3`,
- `map`  returns the location of the memory
- `list(map)` returns the values

```python
# list comprehension can do the same thing
ex = [1,2,3,4,5]
f = lambda x,y: x+y
print(list(map(f,ex,ex)))
# [2,4,6,8,10]

# [sum(x) for x in zip(ex,ex)]
```

```python
list(map(
	lambda x: x**2 if x%2==0 else x,
	ex))
# [1,4,3,16,5]
# 'else' is a must!
```

# Reduce

apply function continuously to elements of list in order

```python
from functools import reduce
print(reduce(lambda x,y: x+y, [1,2,3,4,5]))
# answer : 15
# what it does :
# 1) x=1,y=2 --> x+y=3
# 2) x=previous return,y=3 --> 6
# 3) x=6, y=4 -->10
# 4) x=10, y=5 --> 15!
```

```python
# e.g. factorial
def factorial(n):
	return reduce(
		lambda x,y: x*y, range(1,n+1))
```

# Asterisk *

input undefined length of elements at once (as a tuple)

```python
def asterisk_test1(a, *args):
	print(a,args)
asterisk_test1(1,2,3,4,5,6)

# 1 (2,3,4,5,6)
# type(args) : tuple

def asterisk_test2(a, **kargs):
	print(a,kargs)
asterisk_test2(1,b=2,c=3,d=4,e=5,f=6)

# 1 {'b':2,'c':3,'d':4,'e':5,'f':6}
# type(kargs) : dict
```

## Unpacking

```python
# * : unpack and insert
print(1,*(2,3,4,5,6))
# 1 2 3 4 5 6
```

```python
def asterisk_test3(a,b,c,d,e=0):
	print(a,b,c,d,e)

data = {"d":1, "c":2, "b":3, "e":56}
asterisk_test3(10,**data)
# 10 3 2 1 56
```

# Collections

library of data structures

## deque

stack, queue. more efficient than list

`rotate`, `extend`, `reverse`, etc

## OrderedDict

save in order of input.

Use to order dict by value or key

```python
from collections import OrderedDict

for k,v in OrderedDict(sorted(d.items(), key=lambda t: t[0])).items():
	print (k,v)
# ordered by key
for k,v in OrderedDict(sorted(d.items(), key=lambda t: t[1])).items():
	print (k,v)
# ordered by values
```

## defaultdict

set default value of the dictionary

```python
from collections import defaultdict

d = defaultdict(object)
d = defaultdict(lambda: 0) # set default value to be 0
print(d["first"])
# 0
# even though key "first" was not defined beforehand
```

## Counter

count number of characters in the list (word)
