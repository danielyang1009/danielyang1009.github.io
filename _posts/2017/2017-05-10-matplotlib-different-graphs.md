---
layout: post
date: 2017-05-10
title: Matplotlib Different Graphs
description: Some example of different matplotlib plots
categories: matplotlib
tags: matplotlib python
---

## Scatter plot

```python
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline

n = 1024
# random generate X,Y value
X = np.random.normal(0, 1, n)
Y = np.random.normal(0, 1, n)
# generate color
T = np.arctan2(Y,X)

plt.scatter(X, Y, s=75, c=T, alpha=0.5)
plt.xlim((-1.5,1.5))
plt.ylim((-1.5,1.5))
plt.xticks(())
plt.yticks(())
```
## Bar chart

```python
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline

n = 12
X = np.arange(n)
Y1 = (1 - X / float(n)) * np.random.uniform(0.5, 1.0, n)
Y2 = (1 - X / float(n)) * np.random.uniform(0.5, 1.0, n)

plt.bar(X, +Y1, facecolor='#9999ff', edgecolor='white')
plt.bar(X, -Y2, facecolor='#ff9999', edgecolor='white')

# ha: horizontal alignment
# va: vertical alignment
# where (x,y) is position of our text
for x, y in zip(X, Y1):
    plt.text(x, y + 0.05, '%.2f' % y, ha='center', va='bottom')

for x, y in zip(X, Y2):
    plt.text(x, -y - 0.05, '%.2f' % y, ha='center', va='top')

plt.xlim(-1, n)
plt.xticks(())
plt.ylim(-1.25, 1.25)
plt.yticks(())
```

## Contour Chart

```python
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline

def f(x,y):
    # the height function
    return (1 - x / 2 + x**5 + y**3) * np.exp(-x**2 -y**2)

n = 256
x = np.linspace(-3, 3, n)
y = np.linspace(-3, 3, n)
X,Y = np.meshgrid(x, y)

# use plt.contourf to filling contours
# X, Y and value for (X,Y) point
# camp: color map
# 8: how many ways to fill contour colors
plt.contourf(X, Y, f(X, Y), 8, alpha=.75, cmap=plt.cm.hot)

# use plt.contour to add contour lines
# 8: how many contours to draw
C = plt.contour(X, Y, f(X, Y), 8, colors='black', linewidth=.5)
# adding label
plt.clabel(C, inline=True, fontsize=10)

plt.xticks(())
plt.yticks(())
plt.show()
```

## 3D plot

```python
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D
%matplotlib inline

fig = plt.figure()
ax = Axes3D(fig)
# X, Y value
X = np.arange(-4, 4, 0.25)
Y = np.arange(-4, 4, 0.25)
X, Y = np.meshgrid(X, Y)
R = np.sqrt(X ** 2 + Y ** 2)
# height value
Z = np.sin(R)

# rstride: row, cstride: column
# the lower the rstride and cstride value, coarser the mesh
ax.plot_surface(X, Y, Z, rstride=1, cstride=1, cmap='rainbow')
ax.contourf(X, Y, Z, zdir='x', offset=-4,cmap='rainbow')
ax.set_zlim(-2,1.5)
```
