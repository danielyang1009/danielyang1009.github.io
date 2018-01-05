---
layout: post
date: 2018-01-02
title: Compressed Sprase Row
description: What's compressed sprase row?
categories: machine-learning
tags: machine-learning
---

## Sparse matrix

[Sparse matrix](https://en.wikipedia.org/wiki/Sparse_matrix) is a matrix in which most of the elements are zero. In contrast, if most of the elements of an matrix is non-zero, then the matrix is consider to be dense. Because its sparse nature, it consume less memory and it's easy to compute.

## `Scipy.sparse`

In [`scipy.sparse`](https://docs.scipy.org/doc/scipy-0.14.0/reference/sparse.html) library, we have `csr_matrix` class. And we can transform a metrix to its compressed sparse row form by `to_csr()` method. But first we need to figure out what's compressed sparse row and how to construct one.

## Example
Two examples are provided from [`scipy.sparse.csr_matrix`](https://docs.scipy.org/doc/scipy-0.14.0/reference/generated/scipy.sparse.csr_matrix.html#scipy.sparse.csr_matrix).

##### Example 1
```python
>>> row = array([0,0,1,2,2,2])
>>> col = array([0,2,2,0,1,2])
>>> data = array([1,2,3,4,5,6])
>>> csr_matrix( (data,(row,col)), shape=(3,3) ).todense()
matrix([[1, 0, 2],
        [0, 0, 3],
        [4, 5, 6]])
```

To construct/decompose a CSR matrix we need three vectors together to represetn this sparse matrix. A `row` vector, a `col` vector and a `data`/value vector. It's obvious to see that data vector just store all the data value in order, in this case, is `1, 2, 3, 4, 5, 6`. And row and col is just coordinate of data/value in its dense matrix form. For example, first value `1` is locate at row `0` col `0`. And second value `2` is located at row `0` and col `2` and go on.

##### Example 2
```python
>>> indptr = array([0,2,3,6])
>>> indices = array([0,2,2,0,1,2])
>>> data = array([1,2,3,4,5,6])
>>> csr_matrix( (data,indices,indptr), shape=(3,3) ).todense()
matrix([[1, 0, 2],
        [0, 0, 3],
        [4, 5, 6]])
```

In the second example, data store in standard CSR representation. `data` vector still are non-zero value of our matrix.And `indices` is column indices like in previous example. The `indices` value is a bit obscure to understand. `indptr` or indices pointer give us an idea what row data/value belongs to.

In our example we have `[0, 2, 3, 6]` in our `indptr`. It means that `data[0:2]` which is `1,2` in our `data` vector are contained in row 0. And `data[2:3]` which is `3` is contained in row 1. And last, `data[3:6]` which is `4, 5, 6` is contained in row 2.

Therefore we can see:
- Row 0: 1, 2
- Row 1: 3
- Row 2: 4, 5, 6

Since we have establish which number is in which row. Then we can just use `indices` vector to arrange those numbers in different row to its correct column position like we did in example 1.

It could be silly if you just have a small matrix like this example. But you get to very large matrices with lots of zeroes, this representation is going to make sense.
