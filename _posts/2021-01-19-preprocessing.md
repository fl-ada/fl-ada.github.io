---
title: "Preprocessing"
permalink: /blog/tf_04/
date: 2021-01-19 15:42
background:

categories:
  - blog
tags:
  - blog
  - python
  - tensorflow
  - deeplearning
last_modified_at: 2021-01-18T15:43:54+09:00
---

Lecture from 

[텐서플로우로 시작하는 딥러닝 기초](https://www.boostcourse.org/ai212)

---

# Learning rate

![https://www.jeremyjordan.me/content/images/2018/02/Screen-Shot-2018-02-24-at-11.47.09-AM.png](https://www.jeremyjordan.me/content/images/2018/02/Screen-Shot-2018-02-24-at-11.47.09-AM.png)

normal learning rate = 0.01, 3e-4=0.0003

## learning rate decay

adjust the learning rate when the model is stuck before reaching the minimum point

- step decay
- exponential decay

```python
learning_rate = tf.train.exponential_decay(starter_learning_rate, global_step, 1000, 0.96, )
# 1000 : for every 1000 steps
# 0.96 : adjuestment
# exp_rate = starter_rate * exp(-0.96 * t)
tf.train.inverse_time_decay
tf.train.natrual_exp_decay
tf.train.piecewise_constant
tf.train.polynomial_decay
```

# Preprocessing

## Feature Scaling

### standardization

<img src="https://render.githubusercontent.com/render/math?math=\displaystyle x_{new}=\frac{x-\mu}\sigma">

### normalization

<img src="https://render.githubusercontent.com/render/math?math=\displaystyle x_{new}=\frac{x-x_{min}}{x_{max}-x_{min}}">

## Noisy Data

can solve by extracting only the important part

e.g.

Will you order a pizza or something..? → you order pizza (NLP)

Photo → crop only the face part (face recognition)

# Overfitting

trained fitting to **training data** too much

- get more training data (helps to fix **high var**)

    e.g. image

    - color jittering
    - horizontal flips
    - random crops or scales
- smaller set of features (dimentionality reduction-PCA) (fixess high var)

    ```python
    from sklearn.decompostion import PCA
    pca = decomposition.PCA(n_components=3)
    pca.fit(X)
    X = pca.transform(X)
    ```

## Underfitting

- add additional features (when hypo is too simple) (fixes high bias)

## Regularization

adding term to loss

![eq_regularization.png](/assets/images/posts/2021-01-19/eq_regularization.png)

```python
# L2 loss
tf.nn.l2_loss(features)
```

---

## Dropout and Batch Normalization

in a post later