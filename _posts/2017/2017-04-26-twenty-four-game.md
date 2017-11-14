---
layout: post
date: 2017-04-26
title: Twenty-four Game
description: Thought and solution of 24 game
categories: algorithm
tags: algorithm
---

## 24 Game

Basic goal of 24 game is to manipulate four cards so that the end result is 24. For example: `[11, 8, 3, 5]` will be `(11-9)*(3+5) = 24`. Since original version of 24 is player with ordinary deck of playing cards. Therefore, the integer will be from `1` to `13`.

Reference: [24 Game](https://en.wikipedia.org/wiki/24_Game)

- Number: from `1` to `13`
- Operator:
  - Addition
  - Subtraction
  - Multiplication
  - Division
  - Parentheses

## Thoughts

First thought of solve this problem will be using brute-force. For number can be only used once, there are `4^4 = 256` ways to pick cards. We can only use 3 operators between 4 numbers. There are `4^3 = 56` ways, if we don't count parentheses yet. There are 5 ways to add parentheses:

- `((AB)C)D`
- `(A(BC))D`
- `(AB)(CD)`
- `A((BC)D)`
- `A(B(CD))`

Therefore, we have a total of `4^4 * 4^3 * 5 = 81,920` ways to place our numbers and operators.
