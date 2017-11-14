---
layout: post
date: 2017-04-15
title: Python Generator
description: Basic introduction of python generator
categories: python
tags: python
---

## Introduction

In python language, generator is, without doubt one, one of most useful feature. Meanwhile, it is most unused feature. It's a new concept that no other main stream language like C/C++ or Java has this feature. Therefore it doesn't bring much attention. On the other side, it increase learning cost of software engineers. Eventually, it causes people to let this useful feature slip.

## Iteration Protocols

Because generator automatically implement iteration protocols, and iteration protocols is quite a new concept. Therefore, to better understanding of generator, we need to review the concept of iteration protocols.

1. Iteration Protocols: object need to provide a next method, it will either return next item, or it will rise a `StopIteration` exception to stop iteration.
2. Iterable object: object that conforms to the iterator protocol, which means they provide two methods: `object.__iter__()` and `object.next()`
3. Protocol: which define rules to access objects. In Python built-in functions(like, for loops, sum, min, max, etc.) uses iteration protocols to access iterable objects

For example: In all language we can use for to traverse array. Python list is an array. Therefore we can traverse a list using for loops.

```python
for n in [1, 2, 3, 4,]:
    print(n)
```

However, if you are familiar with python, you will know that you can also use for to traverse file object.

```python
with open('/files/myfile') as f:
    for line in f:
        print(line)
```

But why in python, you can use for to traverse file? This is because in python, file objects implement interation protocal. for Loop don't know it's a file object or not. It just accesses objects using interation protocal. And we can easily access to files.

## Generator

Python uses generator to provide delayed operation, which is only yield result when needed. It doesn't yield result immediately. This is the main advantage of using a generator.

Generator Function: like defining normal function, however, it uses yield instead of return to return result. yield statement only return one result at time, and between each result, function is pause, in order to continue next time when it needs to yield the next result.
Generator Expression: similar to list comprehension. The difference is that generator expression yield only one result at one time, unlike list comprehension which yield all result immediately.

### Generator Function

Here is example using generator to return square of natural numbers.

- Using generator

```python
def gensquares(N):
    for i in range(N):
        yield i ** 2

for item in gensquares(5):
    print(item)
```

- Using function

```python
def gensquares(N):
    res = []
    for i in range(N):
        res.append(i*i)
    return res

for item in gensquares(5):
    print(item)
```

We can see that we write less code using generator, and it is more pythonic.

### Generator Expression

If we use list comprehension, it will return all result at once.

```python
>>> squares = [x ** 2 for x in range(5)]
>>> squaress
[0, 1, 4, 9, 16]
```

When change square brackets to parenthesis, we have generator expression

```python
>>> squares = (x ** 2 for x in range(5))
>>> squares
<generator object <genexpr> at 0x000002C8CA267D8>
>>> next(squares)
0
>>> next(squares)
1
>>> next(squares)
4
>>> list(squares)
[9, 16]
>>> next(squares)
StopIteration
```

Python uses iteration protocol to make `for` become more universal. And most built-in function in python also use iteration protocol. For example, sum is python built-in function and it also use iteration protocol. Therefore when we want to `sum` a list.

```python
sum(x ** 2 for x in range(4))
```

```python
sum([x ** 2 for x in range(4)])
```

## Examples

To understand the advantage of generator, we can see following two examples.

### Memory usage

Like mentioned before, one most important advantage of generaotr is it yield one result at one time. It will be important to deal with large amount of data. We can compare the memory usage of following two expression.

```python
sum([i for i in range(1000000000])
sum(i for i in range(1000000000)
```

For first case, my computer stuck immediately. However for second case, we use generator expression, we use much less memory.

### Readability

In this example, we want to know the position of words in text.

- When not using generator
```python
def index_words(text):
    result = []
    if text:
        result.append(0)
    for index, letter in enumerate(text, 1):
        if letter == ' ':
            result.append(index)
    return result
```

- When using generator
```python
def index_words(text):
    if text:
        yield 0
    for index, letter in enumerate(text, 1):
        if letter == ' ':
            yield index
```

We can see from two reasons in above examples, using generator improve readability and more pythonic

1. We have less code.
2. In the case not using generator, we need to `result.append(index)` first, before we return `index`. It's more clear that we want to return `index` in the case of using generator.

# Precautions

In this case, we want to know the percentage of population by state. Therefore we need to sum up population in eachstate, then divide by total population.

```python
def get_states_population(filename):
    with open(filename) as f:
        for line in f:
            yield int(line)

gen = get_states_population('data.txt')
total_population = sum(gen)

for population in gen:
    print population / total_population
```

If we execute the code above, we won't have any output. This is because generator can only be traverse once. When we execute sum statement, we have already traverse our generator. Therefore when we try to traverse our generator again to calculate percentage, we won't have any output. Therefore, the only thing we need to be careful is that <strong>generator can only be traverse once.</strong>
