---
layout: post
date: 2017-11-06
title: 1000 People In A Circle
description: Brainteaser of 1000 people in a circle
categories: brain-teaser
tags: brain-teaser
---

## The Story

Here is a brainteaser that bothers me a while. Didn't solve it at first time but using Excel. Now I see this brainteaser again. I will trying to solve it just using simple mathematics.

"1000 people are standing in a circle, all numbered from 1 to 1000. Person 1 has a gun which he kills person 2 and give person 3 the gun. It goes on and on. Person 3 kills person 4 and passes the gun to person 5. This continues until there is only one person alive. Who is the last standing man?"

## Simple Math

First, observe a simple case, if only one person (n=1) then the survivor will be himself.

Second, if there are two person (n=2), the survivor will be person 1 as well.

For n=4 case, the survivor is still person 1. And so on. If the total number of person is `2^n` then survivor will be person 1.

Then if we need to transfer our n=1000 case to either n=512 `2^9` or n=1024 `2^10` case, the problem will be dramatically simplified, which provide us two ways of examining this problem.

Then our problem become "who has the gun with remaining total number of people is 512, who is the survivor." And we will know that `1000-512=488`. So after 488 people killed, the next person who has the gun is the survivor. And apparently this person is `488*2+1=977`.

We can also transfer our n=1000 case to n=1024 `2^10`  case, which we know for sure the survivor is person 1. Now, we can consider a case of 1024 people but first 24 people are killed, then the total number of people is 1000. And this is the number what we want. Then our circle become `1 3 5 .... 47 49 50 51 ... 1024` which `2 4 6 ... 46 48` 24 people have been killed. If we start from this situation, the total number of people is 1000. And our circle become `49 50 51 ... 1024 1 3 5 7 ... 45 47`. But we know for sure that person 1 is going to be the survivor. Then our problem has became "what is the position of person 1 in this new circle". And person 1's position in our new circle is `1000-24+1=977`.

## Complex Python

This is a solution using Python to create a link list to solve this problem. This will print out the order of each kill and the last man standing.

```python
class Node(object):
	def __init__(self, value):
		self.value = value
		self.next = None

def create_linkList(n):
	head = Node(1)
	ptr = head
	for i in range(2, n+1):
		newNode = Node(i)
		ptr.next= newNode
		ptr = newNode
	ptr.next = head
	return head

n = 1000 # total number of people
m = 2 # kill the second person
if m == 1: # if m==1 then the last person is nth person
	print(n)
else:
	head = create_linkList(n)
	ptr = None
	cur = head
	while cur.next != cur: # if points to itself then terminate
		for i in range(m-1):
			ptr =  cur
			cur = cur.next
		print(cur.value)
		ptr.next = cur.next
		cur.next = None
		cur = ptr.next
	print(cur.value)
```

## Josephus problem

After spent a while of exploring the internet, I found this is a problem call "Josephus problem" or "Josephus permutation". There is more detail solution of this problem can be found from [Wikipedia](https://en.wikipedia.org/wiki/Josephus_problem).
