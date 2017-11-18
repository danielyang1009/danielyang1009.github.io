---
layout: post
date: 2017-05-13
title: Python String Format
description: Python string format basics
categories: python
tags: python
---

## Intro

Everything I want to format string output, I look up online. This time I want to put everything that I frequently use in the post.

Reference: [Pyformat](https://pyformat.info/)

### New formatting

#### Basic
```python
'{}-{}'.format('one', 'two')
```

```
one two
```

#### Rearrange

```python
'{1}-{0}'.format('one', 'two')
```

```
two one
```

## Number formatting
```
|     Number | Format  |    Output | Description                                   |
|------------|---------|-----------|-----------------------------------------------|
|   3.141592 | {:.2f}  |      3.14 | 2 decimal places                              |
|  3.1415926 | {:+.2f} |     +3.14 | 2 decimal places with sign                    |
|         -1 | {:+.2f} |     -1.00 | 2 decimal places with sign                    |
|    2.71828 | {:.0f}  |         3 | No decimal places                             |
|          5 | {:0>2d} |        05 | Pad number with zeros (left padding, width 2) |
|          5 | {:x<4d} |      5xxx | Pad number with x’s (right padding, width 4)  |
|         10 | {:x<4d} |      10xx | Pad number with x’s (right padding, width 4)  |
|    1000000 | {:,}    | 1,000,000 | Number format with comma separator            |
|       0.25 | {:.2%}  |    25.00% | Format percentage                             |
| 1000000000 | {:.2e}  |  1.00e+09 | Exponent notation                             |
|         13 | {:10d}  |        13 | Right aligned (default, width 10)             |
|         13 | {:<10d} |        13 | Left aligned (width 10)                       |
|         13 | {:^10d} |        13 | Center aligned (width 10)                     |
```

## Convert values to different bases

```python
print("{0:d} - {0:x} - {0:o} - {0:b} ".format(21))
```

```
21 - 15 - 25 - 10101
```

## More tricks

### Named arguments

```python
madlib = " I {verb} the {object} off the {place} ".format(verb="took", object="cheese", place="table")
```

```
I took the cheese off the table
```

### Reuse same variable multiple times

```python
str = "Oh {0}, {0}! wherefore art thou {0}?".format("Romeo")
```

```
Oh Romeo, Romeo! wherefore art thou Romeo?
```

### Use format as a function

```python
## defining formats
email_f = "Your email address was {email}".format

## use elsewhere
print(email_f(email="bob@example.com"))
```


### Escaping braces

```python
print(" The {} set is often represented as {% raw %}{{0}}{% endraw %}".format("empty"))
```

```
The empty set is often represented as {0}
```
