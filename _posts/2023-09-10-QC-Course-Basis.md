---
layout: post
title: Basic Mathematics For Quantum Mechanics - Basis and Linear Combinations
author: Charles Thomas
---

## What is a linear combination?
We have talked about how in a vector space you can add vectors together and multiply them together. These two operations allow us to talk about linear combinations of vectors 

Given two vectors v and w we know that

$$z = av + bw$$

Where a and b are scalars is also a vector. We say that z is a linear combination of v and w. 

So a linear combination is just a combination of two (or more) vectors using only vector addition and scalar multiplication. 

So consider the two vectors:


$$v = \begin{bmatrix}3 \\ 4 \\ 7\end{bmatrix}$$

$$w = \begin{bmatrix}5 \\ 8 \\ 1\end{bmatrix}$$

Then

$$4v + 5w = 4\begin{bmatrix}3 \\ 4 \\ 7\end{bmatrix} + 5\begin{bmatrix}5 \\ 8 \\ 1\end{bmatrix} = \begin{bmatrix}37 \\ 56 \\ 33\end{bmatrix}$$


## What is the span of a linear combination?
Given two vectors v and w we can ask what are all the vectors we can from them using linear combinations. The set of all vectors we can make from them is called the span. 

Returning to

$$v = \begin{bmatrix}3 \\ 4 \\ 7\end{bmatrix}$$

$$w = \begin{bmatrix}5 \\ 8 \\ 1\end{bmatrix}$$

The span of these vectors is the following set:

$$\{a \begin{bmatrix}3 \\ 4 \\ 7\end{bmatrix} + b\begin{bmatrix}5 \\ 8 \\ 1\end{bmatrix} | a, b \in \mathbb{R} \}$$

We can even consider the span of more than two vectors in fact given a set of vectors we can ask what is the span of all the vectors in the set


## What is linear independence? 
Given a set of a vectors P and a vector c, we can ask if c is in the span of P 

If c is not in the span of P then we say c is linearly independent of P because we cannot write it as a linear combination of the vectors in P. 

If c is in the span of P then we day it is linearly dependent. 


## Linearly independent set 
Given a set of vectors we can ask if I take a vector out of the set is it linearly independent to all the other vectors. 

If every vector in a set is linearly independent from every other vector in the set then we say that the set is linearly dependent 

## What is a basis?
Given a vector space, we can ask if there is a set of vectors such that they span the whole space. 

In other words, can we make all the vectors in the vector space out of some smaller subset of the vectors. 

We can now impose another restriction on our set of vectors: that the set is linearly independent. 

If there is a linearly independent set of vectors that spans the whole space we call that set a basis 

Let's take a look at a simple example

$$\{ \begin{bmatrix}1 \\ 0\end{bmatrix}, \begin{bmatrix}0 \\ 1\end{bmatrix}\}$$

This is a basis as we can write any vector as a linear combination of them

$$\begin{bmatrix}a \\ b\end{bmatrix} = a\begin{bmatrix}1 \\ 0\end{bmatrix} + b\begin{bmatrix}0 \\ 1\end{bmatrix}$$

And they are linearly independent from each other as we can't write one in terms of the other

## Understanding column vectors
Column vectors can be a little bit confusing because we use them in kind of ways. 

The first way, we use them is just as a list of numbers. This works well in many of the vector spaces we've come across so far. But for the more complicated vector spaces that we're going to see this doesn't quite work.

So let's start by remembering that if I have some basis

$$b_1, b_2, ... b_n$$

Then I can write any vector using them

$$v = a_1b_1 + a_2b_2 + ... a_ib_i$$

where the a's are scalars

So if you and I agree on a basis ahead of time then when I want to tell you about a vector I need to tell you all the a's


We can write all the a's as a column which is our column vector so:

$$\begin{bmatrix}a_1 \\ a_2 \\ ... \\ a_i\end{bmatrix} = a_1b_1 + a_2b_2 + ... a_ib_i$$

So all a column vector is, is a representation of a vector using a particular basis. The using a particular basis bit is really important as if you and I are using different basis then we will mean different things when writing down the same column vector.