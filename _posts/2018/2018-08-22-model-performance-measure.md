---
layout: post
date: 2018-08-22
title: Model Performance Measure
description: How to meausre model performance
categories: machine-learning
tags: machine-learning
---

## Intro

When measuring performance of a model, it's to easy to think of indicators like accuracy(the percentage of correctly classified observations) or error rate(the percentage of wrong classified observations). However we need more indicators to measure model performance to answer in-depth questions.

## Precision, recall

To better understand precision, recall and F1, the following table demostrate an example of real world situation, where TP/NP is true/false positve and TN/FN is true/false nagetive. For example, a positive example if we classify it correctly, then it's a true positive. However, if we classify wrongly, it is a nagetive positive.

It may seems confusion when mentioning true/positve, false/negative. In this case, we may predetermine a threshold or a cut point which split our predictions in two. Usually we define predictions that above threshold as "positve", below threhold as negative. True and false is easy to understand. True is when we predict correctly, false when predict wrongly.

| Positive obs | Negative obs |
|:---:|:---:|
|*TP*|**FP**|
|*TP*|TN|
|...|...|
|*TP*|TN|
|**FN**|TN|

Just notice first row, if we predict a negative ob as postive, it becomes a false positve. And in last row, if we predict a postive ob as negative, it creates a false nagetive. Clearly we have `TP + FP + TN + FN = total samples`.

After we define TP, FP, TN and FN, we can define what `precision` and `recall` is.

**P(查准率) = TP / (TP + FP)**

We can see that `precision` defines in all we predict as postive, what percentage is truely postive obs(predict correctly).

**R(查全率) = TP / (TP + FN)**

And `recall` defines in all positive observations, what percentage we predict correctly.

## P-R graph and BEP

It's usually hard to get precision rate and recall rate both high. We can graph recall rate as x-axis, and precision rate as y-axis, to measure performance of a model. This graph is called `P-R graph`. If graph of one model is "surrounded" by another model, it's clearly the latter model is better. Since latter model is higher in both precision rate and recall rate. However, it's possible the graphs of two models have interception. Then it's hard to definitely determine which model is better. It's easy to think that the model with bigger area underneath is better. However, this area is usally difficult to calculate. In this case, we can calcuate a `break-even point(BEP)` where precision = recall. In result, higher BEP value indicates better model performance.

## F1

With F1 solves our problem of performance measurement. It's considered to be over-simplied. F1 indicator is the one we usually used.

**F1 = 2\*P\*R / (P+R)**

F1 is defined by the harmonic mean of precision and recall.

**1/F1 = 1/2 (1/P + 1/R)**

In this model, we have the same weight of precision and recall, which is 1/2. Moreover, in other applications, we may value them differently. In merchandise recommandaion system, it's important to cause less disturbance. It requires higher precision rate, which is in all the users we targets, higher percentage of users are truely the target audience who have higher chance to buy that specific merchandise.

In some applications, like criminal screening system. It values recall rate more. We want to filter more true criminals(less outlaws) in percentage of our criminal preditions.

Therefore we have more general version of F1 indicator, F_beta.

**F_b = (1+b^2)\*P\*R / (b^2\*P + R)**

This equation is also define by harmonic mean.

**1/F_b = 1/(1 + b^2)[1/P + b^2/R]** *where b>0*

Beta determines the weight of precision and recall. When beta>1, we value recall more. When beta<1, we value precision more.

## ROC and AUC

As we already defined TP, FP, TN and FN, we can continuely define two more which are described in `ROC(receiver operating characteristic)` curve. If we graph TPR in y-axis, and NPR in x-axis, we have ROC curve, a upward sloping curve. And the area under curve is called `AUC`.

**TPR(True Positive Rate) = TP / (TP + FN)**

TPR is the same as R(recall) =  TP / (TP + FN), which calculate in all positive observations, how many we predict/pick correctly.

**FPR(False Positive Rate) = FP / (FP + TN)**

In contrast, we have FPR which describe in all negative observations, how many we predict/pick wrongly, hence false.

| Positive obs| Negative obs|
|:---:|:---:|
|**TP**|*FP*|
|**TP**|*TN*|
|...|...|
|**TP**|*TN*|
|**FN**|*TN*|

When comparing ROC curve, is same as comparing P-R curve. The bigger AUC(area under curve), the better.