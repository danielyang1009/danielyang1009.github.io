---
layout: post
date: 2018-01-04
title: Compressed Sprase Row
description: What's compressed sprase row?
categories: machine-learning
tags: machine-learning
---

## Sparse matrix

[Sparse matrix](https://en.wikipedia.org/wiki/Sparse_matrix) is a matrix which most of the elements are zero. In contrast, if most of the elements of an matrix is non-zero. Then the matrix is consider to be dense. Because its sparse nature, it consume less memory and it's easy to compute.

## `Scipy.sparse`

In [`scipy.sparse`](https://docs.scipy.org/doc/scipy-0.14.0/reference/sparse.html) library, we have `csr_matrix` class. And we can transform a metrix to its compressed sparse row or CSR representation by `to_csr()` method. We need to figure out what's compressed sparse row and how to construct/decompose one.

There is also compressed sparse column representation or CSC. But they are sharing the same idea. Therefore in this article, I will focus on CSR.

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

To construct/decompose a CSR we need three vectors together to represetn this sparse matrix. In this example a `row` vector, a `col` vector and a `data`/value vector. It's obvious to see that data vector just store all the data value in order, in this case, is `1, 2, 3, 4, 5, 6`. And row and col is just coordinate of data/value in its dense matrix form. For example, first value `1` is locate at row `0` col `0`. And second value `2` is located at row `0` and col `2` and go on.

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

In this second example, data store in standard CSR representation. `data` vector still are non-zero value of our matrix. And `indices` is column indices like `col` vector in previous example. The `indices` value is a bit obscure to understand. `indptr` or indices pointer give us an idea what row data/value belongs to.

In our example we have `[0, 2, 3, 6]` in our `indptr` vector. It means that `data[0:2]` which is `1, 2` in our `data` vector are contained in row 0. And `data[2:3]` which is `3` is contained in row 1. And last, `data[3:6]` which is `4, 5, 6` is contained in row 2.

That is:
- row 0: 1, 2
- row 1: 3
- row 2: 4, 5, 6

Since we have establish which number is in which row. Then we can just use `indices` vector to arrange those numbers in different row to its correct column position like we just did in example 1.

It could be silly to do CSR or CSC representation if you just have small matrices like above examples. But once you get to very large matrices with lots of zeroes, this representation is going to make sense.
