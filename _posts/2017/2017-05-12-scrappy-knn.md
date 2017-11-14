---
layout: post
date: 2017-05-12
title: Scrappy KNN
description: Create a simply knn
categories: machine-learning
tags: machine-learning python
---

## Intro

In this post, I'm tryign to build my first machine learning classifier from scratch, which is simple and 'scrappy'. However it will give me a broad impression of to solve a machine learning problem.

I will be using `scikit-learn` and `scipy` package, which provide me the functions I need as well as the dataset. I will be using the famous [wiki: iris dataset](https://en.wikipedia.org/wiki/Iris_flower_data_set). And the dataset is also given in the wiki page. There are four features that help us classify which species of iris flower it is.

There are major step in supervised learning. First is training data: let computer learn from the data. Second is fitting data: let computer predict from our inputed features or X.

- Regression: the output variable takes continuous values.
- Classification: the output variable takes class labels.

## `KNeighborsClassifier`

We first building a `k nearest neighbors` using `KNeighborsClassifier` function from `sklearn`. In this algorithm we just simply look what are the labels of k nearest neighbors, and classify our training data base on majority vote of the neighbors.

Wiki: [k-nearest neighbors algorithm](https://en.wikipedia.org/wiki/K-nearest_neighbors_algorithm)

```python
from sklearn import datasets
from sklearn.model_selection import train_test_split

# load iris dataset
iris = datasets.load_iris()

# X is the feature we use to predict result
X = iris.data
# y is the result
y = iris.target

# split our X, y to 50% as traning data, 50% as testing data
X_train, X_test, y_train, y_test = train_test_split(X, y, train_size=0.5)

sk_clf = KNeighborsClassifier()
# traning our model with X_train, y_train
sk_clf.fit(X_train, y_train)
# using X_test to test our model
sk_predictions = sk_clf.predict(X_test)
# compare prediction accuracy vs result
print('skilearn: {0:.2f} %'.format((accuracy_score(y_test, sk_predictions)*100)))
```

## Scrappy 1NN

Building a simple, bare-born, or 'scrappy' classifier, I continue used method of KNN. However, to simplify, just label it as same as the closest neighbor. And to use euclidean distance to define what the closest neighbor is.

```python
from sklearn import datasets
from sklearn.model_selection import train_test_split
from sklearn.neighbors import KNeighborsClassifier
from sklearn.metrics import accuracy_score
from scipy.spatial import distance

# calculate euclidean distance
def euc(a, b):
    return distance.euclidean(a, b)

class ScrappyKNN():
    # scrappy fit, just initial our class
    def fit(self, X_train, y_train):
        self.X_train = X_train
        self.y_train = y_train

    def predict(self, X_test):
        prediction = []
        for row in X_test:
            # find the label of closest neighbor
            prediction.append(self.closest(row))
        return prediction

    def closest(self, row):
        # initial
        best_distance = euc(row, self.X_train[0])
        best_index = 0
        # range over all point to determine which is closest
        for i in range(1, len(self.X_train)):
            dist = euc(row, self.X_train[i])
            if dist < best_distance:
                best_distance = dist
                # record index
                best_index = i
        # return the label of closest neighbor
        return self.y_train[best_index]

iris = datasets.load_iris()

X = iris.data
y = iris.target

X_train, X_test, y_train, y_test = train_test_split(X, y, train_size=0.5)

sk_clf = KNeighborsClassifier()
sk_clf.fit(X_train, y_train)
sk_predictions = sk_clf.predict(X_test)


sp_clf = ScrappyKNN()
sp_clf.fit(X_train, y_train)
sp_predictions = sp_clf.predict(X_test)


print('skilearn: {0:.2f} %'.format((accuracy_score(y_test, sk_predictions)*100)))
print('scrappyKNN: {0:.2f} %'.format((accuracy_score(y_test, sp_predictions)*100)))
```
