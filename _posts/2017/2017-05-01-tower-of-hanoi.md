---
layout: post
date: 2017-05-01
title: Tower of Hanoi
description: Recursive solution of classic problem tower of hanoi
tags: algorithm python
categories: algorithm
---

## Problem

This classic problem `Tower of Hanoi` help us better understand way to recursive solve a problem. By first divide it into small same problem, then conquer it little by little. Often call `divide and conquer` principle of providing a recursive solution.

Ref: [By Prof. Eric Grimson](https://www.youtube.com/watch?v=rVPuzFYlfYE)

## Code

```python
# Tower of Hanoi
# Three towers A, B, C
# All discs start with A
# Goal: move all discs to C
# Rule:
# 1. Can only move one disc at a time
# 2. Larger disc can never cover up a small disc


def move(n, fr, sp, to):
"""
fr: from, tower A
sp: spare, tower B
to: to, tower C
"""
    if n == 1:
        # if only one disc in A
        # just move it to C
        print(fr, '->', to)
    else:
        # otherwise do recursion
        # move all (n-1) discs except bottom one
        # from A to B
        move(n - 1, fr, to, sp)
        # move the bottom (1) disc
        # from A to C
        move(1, fr, sp, to)
        # move the rest (n-1) discs
        # from B to C
        move(n - 1, sp, fr, to)

move(4, 'A', 'B', 'C')
```

## Detail
```
# n = 4
  Step 1, n = 3:
    Step 1, n = 2:
      1: A -> B
      2: A -> C
      3: B -> C
    Step 2, n = 1:
      A -> B
    Step 3, n = 2:
      1: C -> A
      2: C -> B
      3: A -> B
  Step 2, n = 1:
    A -> C
  Step 3, n = 3:
    Step 1, n = 2:
      1: A -> B
      2: B -> A
      3: C -> A
    Step 2, n = 1:
      B -> C
    Step 3, n = 2:
      1: A -> B
      2: A -> C
      3: B -> C
```
