---
title: "Data Preprocessing"
permalink: /blog/python_05/
date: 2021-01-05 20:01
background:

categories:
  - blog
tags:
  - blog
  - python
last_modified_at: 2021-01-05T20:02:39+09:00
---

studied with the lecture below: 

[머신러닝을 위한 파이썬](https://www.boostcourse.org/ai222/lecture/24523)

---

When operation can be done only for numpy array : `df.tolist() : df to numpy array`

# Missing Data

- drop row : `df.dropna()`
- drop if missing count > n `df.dropna(thresh=n)`
- drop feature if it doesn't have much data
- fill with mean, median, mode : `df.fillna(df.mean())`

# Category

## One-Hot Encoding

vectorize to make binary data

- `pd.get_dummies(df)` : transform all object columns

## Ordinary

numbers do not mean → categorize with dict → One-hot encoding 

## binning

separate data into ranges

```python
pd.cut(df, bins, labels = group_names)
# bins : e.g. [0,25,50,75,100]
```

# Feature scaling

Scale difference too big

- min-max normalization (new: 0~1)
- standardization (Z-score norm)

```python
from sklearn import preprocessing
preprocessing.StandardScalar().fit(df[['cols']])
# StandardScalar(), MibMaxScalar()
```