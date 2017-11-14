---
layout: post
date: 2017-09-17
title: Pandas Indexing
description: comparing different pandas indexing method
categories: python
tags: python pandas
---

## Intro

There are few method we can access our DataFrame with pandas. There are `.ix`, `.loc` and `.iloc`. We will examine them one by one.

## `.ix`

Since `.ix` is deprecated right now. And `.loc`, `.iloc` are expected replacements. `.ix` is a mixture of `.loc` and `.iloc` which supports mixed integer and label based indexing. We will focus more time with `.loc` and `iloc` instead of `.ix`.

## `.loc`

Label-location based indexing

### Basic

It has the basic format of `pd.DataFrame.loc[<row(s)>,<column(s)>]`. If we want to select single row of some DataFrame we created. We can use `myDataFrame.loc[0,:]`. Since it starts with number **0**. And colon (:) means selecting all columns. If we want to select certain rows or columns. We can use `myDataFrame.loc[[0,1,2],:]` or `myDataFrame.loc[0:2,:]` to select row 0,1,2 and all columns. And please notice that when we use `0:2` colon expression, it will include both endpoints (both 0 and 2), unlike `range(0,2)`, only include left endpoint, not right endpoint (only 0, not 2). Or we want to select certain columns, we can use `myDataFrame.loc[:,['col_name1','col_name3']]` will only select two columns of 'col_name1' and 'col_name2'. We also can select consecutive columns using `myDataFrame.loc[:,'col_name1':'col_name3']` to select three columns of 'col_name1' to 'col_name2'.

### Boolean Selection

To select observations with State column equal to 'New York', we can use `myDataFrame.loc[myDataFrame.State=='New York',:]`.


## `.iloc`

Integer-location based indexing

### Basic

It has the same format as `.loc` of `pd.DataFrame.iloc[<row(s)>,<column(s)>]`. To select single of multiple rows or columns, we can use `myDataFrame.iloc[:,[0,3]]` to select all rows and first column(0) and forth column(3). We can also use `0:3` colon expression. However in this case, it's inclusive from left endpoint but **exclusive** from right endpoint like `list(range(0,3))`. In this case `0:3` will show only 0,1,2 columns. You can also do a boolean selection like `.loc` in `.iloc`.
