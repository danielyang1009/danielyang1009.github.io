---
layout: post
date: 2017-05-09
title: Matplotlib Annotation
description: Matplotlib annotation
categories: matplotlib
tags: matplotlib python
---

## Annotation

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(-10, 10, 100)
y = 2 * x + 1
plt.figure(1,figsize=(8,5))
plt.xlim(-5,5)
plt.ylim(-10,10)
plt.plot(x,y)

# setting our axis
ax = plt.gca()
ax.spines['top'].set_color('none')
ax.spines['right'].set_color('none')
ax.spines['bottom'].set_position('zero')
ax.spines['left'].set_position('zero')

# plot a point
x0 = 1
y0 = 2*x0 + 1
plt.scatter(x0,y0,color='b')

# plot two point (x0,y0) and (x0,0)
# `k--` is black dash line
plt.plot([x0,x0],[y0,0],'k--',lw=2.5)

# xy: (x,y) point to annotate
# xycoords: the coordinate system that xy is given, 'data' is default
# the coordinate system that text xytext is given
# xytext: (x,y) to place the text  
# arrowprops: arrow style etc
plt.annotate('2x+1=3', xy=(x0,y0), xycoords=('data'), xytext=(+30,-30), textcoords='offset points', fontsize=16, arrowprops=dict(arrowstyle='<-', connectionstyle='arc3, rad=0.2'))
```
