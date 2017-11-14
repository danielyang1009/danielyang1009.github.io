---
layout: post
date: 2017-05-11
title: Matplotlib Subplot
description: matplotlib subplot
categories: python
tags: matplotlib python
---

## Basic Method
### Example 1

```python
import matplotlib.pyplot as plt

plt.figure(figsize=(6, 4))
# plt.subplot(n_rows, n_cols, plot_num)
# Divide to 2 row, 2 col, and graph at (1,1) position
plt.subplot(2, 2, 1)
plt.plot([0, 1], [0, 1])

# graph at (1,2) position
plt.subplot(222)
plt.plot([0, 1], [0, 2])

# graph at (2,1) position
plt.subplot(223)
plt.plot([0, 1], [0, 3])

# graph at (2,2) position
plt.subplot(224)
plt.plot([0, 1], [0, 4])

plt.tight_layout()
```
### Example 2

```python
import matplotlib.pyplot as plt

plt.figure(figsize=(6, 4))
# divide to 2 rows, 1 col, graph at first (1,1) position

plt.subplot(2, 1, 1)
plt.plot([0, 1], [0, 1])

# divide to 2 rows, 3 cols,
# at this time, first graph will be occupied position (1,1), (1,2), (1,3)
# therefore we start with 4th graph, with position (2,1)
plt.subplot(234)
plt.plot([0, 1], [0, 2])

# graph at (2,2) position
plt.subplot(235)
plt.plot([0, 1], [0, 3])

# graph at (2,3) position
plt.subplot(236)
plt.plot([0, 1], [0, 4])

plt.tight_layout()
```

## Method `subplot2grid`

```python
import matplotlib.pyplot as plt
import matplotlib.gridspec as gridspec

plt.figure()
# with 3x3 grid, starts at (0,0), with column span of 3
ax1 = plt.subplot2grid((3, 3), (0, 0), colspan=3)
ax1.plot([1, 2], [1, 2])
ax1.set_title('ax1_title')
ax2 = plt.subplot2grid((3, 3), (1, 0), colspan=2)
ax3 = plt.subplot2grid((3, 3), (1, 2), rowspan=2)
ax4 = plt.subplot2grid((3, 3), (2, 0))
ax4.scatter([1, 2], [2, 2])
# set_xlabel() and set_xlim() in subplot
# compare to plt.xlabel(), plt.xlim() in figure
ax4.set_xlabel('ax4_x')
ax4.set_ylabel('ax4_y')
ax4.set_xlim(0,3)
ax5 = plt.subplot2grid((3, 3), (2, 1))
```
## Method `gridspec`

```python
import matplotlib.pyplot as plt
import matplotlib.gridspec as gridspec

plt.figure()
gs = gridspec.GridSpec(3, 3)
# use index from 0
ax6 = plt.subplot(gs[0, :])
ax7 = plt.subplot(gs[1, :2])
ax8 = plt.subplot(gs[1:, 2])
ax9 = plt.subplot(gs[2, 0])
ax10 = plt.subplot(gs[-1, -2])
```

## Method `subplots`

```python
# share x axis, share y axis
# It's `subplots` in plural, not `subplot`
f, ((ax11, ax12), (ax13, ax14)) = plt.subplots(2, 2, sharex=True, sharey=True)
ax11.scatter([1,2], [1,2])
ax11.set_xlim(0,3)

plt.tight_layout()
plt.show()
```
