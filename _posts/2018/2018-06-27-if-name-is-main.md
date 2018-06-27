---
layout: post
date: 2018-06-27
title: If name is main
description: Understanding why in python, we use if __name__ == '__main__'
categories: python
tags: python
---

## Why?

Many times we read through python source code and found that there were some weird statments. And I always choose to ignore this statements until I found them everywhere and just want to figure it out.

```python
if __name__ == '__main__':
  main()
```

## To understand

In short, there is an classic explanation which summarize it well.

```
Make a script both importable and executable.
```

To understand this, there are two ways to run a python script. One is to run directly as a script. The other is to run as an imported module, and run from other python script.

Every python module has a variable `__name__`, when we run python script directly, `__name__` is equal to `__main__`, hence, it will then run `main()`. However, if we run as an imported module `__name__` will not equal to `__main__`. Therefore it won't be run.