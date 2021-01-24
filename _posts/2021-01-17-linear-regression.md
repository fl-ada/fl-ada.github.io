---
title: "Linear Regression"
permalink: /blog/tf_01/
date: 2021-01-17 15:31
background:

categories:
  - blog
tags:
  - blog
  - python
  - tensorflow
  - deeplearning
last_modified_at: 2021-01-17T15:51:35+09:00
---

Lecture from 

[텐서플로우로 시작하는 딥러닝 기초](https://www.boostcourse.org/ai212)

---

> *"Regression toward the mean"*

# Linear Regression

## Hypothesis

$$XW=\begin{pmatrix}x_1&x_2&\cdots&x_n\end{pmatrix}\cdot
\begin{pmatrix}w_1\\w_2\\\vdots\\w_n\end{pmatrix}\\
H(X)=XW+b$$

## cost/loss/error

$$\text{avg. of }(H(x)-y)^2$$

$$cost(W,b)=\frac1m\sum_{i=1}^M(H(x_i)-y_i)^2$$

## Goal : $\displaystyle{\argmin_{W,b}cost(W,b)}$

# In TensorFlow

```python
x_data = [1,2,3,4,5]
y_data = [1,2,3,4,5]

# initial values
# usually random
W = tf.Variable(2.9)
b = tf.Variable(0.5)

hypothesis = W * x_data + b
cost = tf.**reduce_mean**(tf.**square**(hypothesis - y_data))
# reduce_mean
#   - reduce : reduce rank
#              y_data : 1D
#              mean : a variable (0D)
```

## Gradient descent

$$\argmin_{W,b}cost(W,b)$$

```python
import tensorflow as tf
tf.enable_eager_execution()

W = tf.Variable(2.9)
b = tf.Variable(0.5)

# alpha, small
learning_rate = 0.01

# update W,b
for i in range(100+1):
	# Gradient descent
	# tape: W, b
	with tf.GradientTape() as tape:
		hypothesis = W * x_data + b
		cost = tf.reduce_mean(tf.square(hypothesis - y_data))
	
	# get derivative(gradient)
	W_grad, b_grad = tape.gradient(cost, [W,b])
	
	# assign_sub : same as {A -= B}
	W.assign_sub(learning_rate * W_grad)
	b.assign_sub(learning_rate * b_grad)
	
	# print every 10
	if i % 10 == 0:
		print("{:5}|{:10.4f}|{:10,4}|{:10.6f}".format(i,W.numpy(),b.numpy(),cost)
```

![fit.png](/assets/images/posts/2021-01-17/fit.png)

minimize the cost → cost gradient = 0

$$\text{include b in matrix W, divide by 2}\\
cost(W):=\frac1{2m}\sum_{i=1}^m(H(x_i)-y_1)^2\\
W:=W-\alpha\frac{\partial}{\partial W}cost(W)\\
=W-\alpha\frac1m\sum_{i=1}^m(W(x_i)-y_i)x_i$$

When cost is convex function, (local min=global min), gradient descent can always find the minimum point.

## Minimizing cost function

```python
X = np.array([1,2,3])
Y = np.array([1,2,3])

def cost_func(W,X,Y):
	hypo = X * W
	return tf.reduce_mean(tf.square(hypo - Y))

W_values = np.linspace(-3,5,num=15)
cost_values = []

for feed_W in W_values:
	curr_cost = cost_func(feed_W,X,Y)
	cost_values.append(curr_cost)
	print("{:6.3f} | {:10.5f}".format(feed_W, curr_cost))
```

![cost func.png](/assets/images/posts/2021-01-17/cost func.png)

```python
# for reproducibility
tf.random.set_seed(0)

X = [1.,2.,3.,4.]
Y = [1.,3.,5.,7.]

W = tf.Variable(tf.random.normal([1], -100., 100.))

for step in range(300):
	hypo = W * X
	cost = tf.reduce_mean(tf.square(hypo - Y))

	alpha = 0.01
	grad = tf.reduce_mean(tf.multiply(tf.multiply(W, X) - Y, X))
	desc = W - tf.multiply(alpha, grad)
	W.assign(desc)

	if step % 10 == 0:
		print('{:5} | {:10.4f} | {:10.6f}'.format(step, cost.numpy(), W.numpy()[0]))

```