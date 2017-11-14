---
layout: post
date: 2017-05-07
title: Matplotlib Figure, Axis and Legend
description: Basic python package matplotlib graph plotting, figure, axis and legend
categories: matplotlib
tags: matplotlib python
---

## Convention

For convenience, we usually shorten the `matplotlib.pyplot` as `plt`. And you need to import the package in python before you can use it. Best environment is to use `jupyter notebook`, which you can run your python code and see the result. Import following two pacakge to start.

```python
import matplotlib.pyplot as plt
import numpy as np
```

## Basic

```python
x = np.linspace(-1,1,50) # put 50 points in [-1, 1]
y = 2 * x # our function
plt.plot(x, y) # plot the graph / create matplotlib object
plt.show() # show it
```

In `jupyter notebook`, one thing to mention is you can put `%matplotlib inline` alongside with other import statment. Then `jupyter notebook` will automatically show the graph. Instand of typing `plt.show()`, to actually show it.

## Figure

In matplotlib, `figure` is the container for our graph. Continue with previous example, if we want to plot two different functions in two different graph. Or graph two different function in same figure

```python
x = np.linspace(-3, 3, 50)
y1 = 2 * x + 1
y2 = x ** 2
y3 = x ** 3

# create a figure, when not numbered with `num=1`
# system will automatically name it by 1, 2, 3, 4...
# set figure, and all following will be graph in same figure
plt.figure(num=1)
plt.plot(x, y1)

# create another figure
# setting figure size by using `figsize`
plt.figure(num=2, figsize=(8,5))
plt.plot(x, y2)
# set color, line width, and line style `--` is dash line
plt.plot(x, y3, color='red', linewidth=3.0, linestyle='--')
```

## Axis
```python
x = np.linspace(-3, 3, 50)
y1 = 2 * x + 1
y2 = x ** 2

plt.figure()
plt.plot(x,y1)
plt.plot(x,y2)

# set x, y shown value range
plt.xlim((-1,2))
plt.ylim((-2,3))

# show x, y axis label
plt.xlabel("X label")
plt.ylabel("Y label")

# show ticks, or matching with text
plt.xticks([-1,0,1,2])
# divide y axis [-2,3] to 5 pa
plt.yticks(np.linspace(-2,3,5),['really bad','bad','normal','good','really good'])

# Moving axis
# gca: get current axis
ax = plt.gca()

# do not show frame/spine of our graph
ax.spines['right'].set_color('none')
ax.spines['top'].set_color('none')

# set ticks position to left and bottom spine
ax.xaxis.set_ticks_position('bottom')
ax.yaxis.set_ticks_position('left')

# move x-axis start with y=-1 position
# move y-axis start with x=0 position
ax.spines['bottom'].set_position(('data',-1))
ax.spines['left'].set_position(('data',0))
```

## Legend

```python
x = np.linspace(-10, 10, 100)
y1 = 2 * x + 1
y2 = x ** 2

plt.figure()
plt.xlim((-1,2))
plt.ylim((-2,3))
l1, = plt.plot(x, y1, label='y1')
l2, = plt.plot(x, y2, linestyle='--', label='y2')

# loc can let matplotlib chose best `loc='best'`
plt.legend(handles=[l1,l2],labels=['2x+1','x^2'],loc='lower right')
```
