---
layout: post
date: 2018-01-02
title: One Hot Encoding
description: What's One Hot Encoding?
categories: machine-learning
tags: machine-learning
---

## Problem

By scikit-learn website [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) will 'Encode categorical integer features using a one-hot aka one-of-K scheme'. That's just completely confusing. In common sense, label encoder should do the following things. Just label everything from 1 to N. And that's what [LabelEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.LabelEncoder.html#sklearn.preprocessing.LabelEncoder) in scikit-learn do.

```
| CompanyName | Category |
|-------------|----------|
| Honda       |     1    |
| Toyota      |     2    |
| VW          |     3    |
```

But there's a problem, in normal label encoding it assumes higher the categorical value better the category. Since if we taking an average of `VW` and `Honda` we're getting `Toyota` ((1+3)/2=2). If we have 100th company, then it's 100 times more weight than `Honda`. And it's not the case at all. So that's why we have one hot encoder, to solve this problem.

## Solution

It's really easy to understand. This will 'binarization' category and put equal weight to every companies to prevent previous problem.

```
| Honda | Toyota | VW |
|-------|--------|----|
| 1     | 0      | 0  |
| 0     | 1      | 0  |
| 0     | 0      | 1  |
```

This is one simple example. And it's quite intuitive. However, this can be quite messy when we have multiple features and each feature has multiple categories as you will see in following example.

## Example

This is the code which provide from scikit-learn. It's not very intuitive to understand. But let's take one step then another to understand what's going on in this example.

##### Code
```python
>>> from sklearn.preprocessing import OneHotEncoder
>>> enc = OneHotEncoder()
>>> enc.fit([[0, 0, 3], [1, 1, 0], [0, 2, 1], [1, 0, 2]])
OneHotEncoder(categorical_features='all', dtype=<... 'numpy.float64'>,
       handle_unknown='error', n_values='auto', sparse=True)
>>> enc.n_values_
array([2, 3, 4])
>>> enc.feature_indices_
array([0, 2, 5, 9])
>>> enc.transform([[0, 1, 1]]).toarray()
array([[ 1.,  0.,  0.,  1.,  0.,  0.,  1.,  0.,  0.]])
```

##### Explanation
```python
>>> enc.fit([[0, 0, 3], [1, 1, 0], [0, 2, 1], [1, 0, 2]])
```
We're fitting an encoder to a set of 4 observations/rows, with 3 features/columns each.

```python
>>> enc.n_values_
array([2, 3, 4])
```
- Feature 1 has 2 possible values: 0, 1
- Feature 2 has 3 possible values: 0, 1, 2
- Feature 3 has 4 possible values: 0, 1, 2, 3

```python
>>> enc.feature_indices_
array([0, 2, 5, 9])
```
Since there are 2+3+4 possible values, the representation is 9 entries long.

- Feature 1 starts at index 0
- Feature 2 starts at index 2 (F1 start + len(F1))
- Feature 3 starts at index 5 (F2 start + len(F2))

```python
>>> enc.transform([[0, 1, 1]]).toarray()
array([[ 1.,  0.,  0.,  1.,  0.,  0.,  1.,  0.,  0.]])
```
We need the `feature_indices_` to properly read this result. Since feature 1 starts at index 0 and feature 2 starts at index 2. Then we know that feature 1 takes space from index 0 to index 2, which is `[1., 0.,]`. We can also do this for feature 2 and 3. Then we have:

- Feature 1 is: [1., 0.]
- Feature 2 is: [0., 1., 0.]
- Feature 3 is: [0., 1., 0., 0.]

In this example we have mapped our 3 features observation to new 9 features/columns dimension with all 0 and 1.

```
Original  ->  Transformed
f1,f2,f3      | f1   | f2      | f3        |
 0, 0, 3  ->  | 1, 0,| 1, 0, 0,| 0, 0, 0, 1|
 1, 1, 0  ->  | 0, 1,| 0, 1, 0,| 1, 0, 0, 0|
 0, 2, 1  ->  | 1, 0,| 0, 0, 1,| 0, 1, 0, 0|
 1, 0, 2  ->  | 0, 1,| 1, 0, 0,| 0, 0, 1, 0|
```

For feature 1, there are two possible categories `0` and `1`, therefore it will be encodered as `[1,0]` for `0` and `[0,1]` for `1` and so on for feature 2 and feature 3.
