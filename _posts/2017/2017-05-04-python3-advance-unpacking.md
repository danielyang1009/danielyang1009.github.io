---
layout: post
date: 2017-05-04
title: Python3 Advance Unpacking
description: Python3 awesome advance unpacking
categories: python
tags: python
---

## Advance Unpacking

```python
>>> a, b, *rest = range(10)
>>> a
0
>>> b
1
>>> rest
[2, 3, 4, 5, 6, 7, 8, 9]
```

Or you can put range in the middle

```python
>>> a, *rest, b = range(10)
>>> a
0
>>> b
9
>>> rest
[1, 2, 3, 4, 5, 6, 7, 8]
```

Or get the first and last lines of a file

```python
>>> with open("using_python_to_profit") as f:
...     first, *_, last = f.readlines()
>>> first
'Step 1: Use Python 3\n'
>>> last
'Step 10: Profit!\n'
```

Or to refactor your functions

```python
def f(a, b, *args):
    # stuff

def f(*args):
    a, b, *args = args
    # stuff
```

Reference: [10 awesome features of Python that you can't use because you refuse to upgrade to Python3](http://www.asmeurer.com/python3-presentation/slides.html#1)
