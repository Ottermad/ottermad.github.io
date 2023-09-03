---
layout: post
title: Basic Mathematics For Quantum Mechanics - Vector Spaces
author: Charles Thomas
---

## Vector Space
A vector space is a collection of two sets and two binary operations.

The first set we'll call V and it is the set of vectors. It can be any set you want. 

The second set we'll call S and is the set of scalars. This means it has to be either the set of real numbers or the complex numbers. (For more advanced readers, technically it can be any field).

The first operation we'll call addition and denote with a + sign. It takes two vectors (two members of our set V) and gives us back a third one.

Using the notation from the earlier post about maps:

$$ + : V \times V \rightarrow V$$

The second operation we'll call scalar multiplication and we'll denote it by \*. It takes one input from the set of scalars and another input from the set of vectors and gives us back a new vector.

$$ * : S \times V \rightarrow V$$

Now both + and * must have some special properties which we'll discuss below but first, we'll look at some examples of vector spaces.

## Examples
Before we dive into the properties of vector addition and scalar multiplication it is helpful to see some examples

From school, you might have been told vectors are columns of numbers such as:

$$\begin{bmatrix} 1 \\ 2 \end{bmatrix}$$

These are vectors in a vector space called

$$\mathbb{R}^2$$

If we have n entries in our columns then they belong to 

$$\mathbb{R}^n$$

In this vector space, we have  defined addition component-wise meaning that we add two vectors by adding the individual numbers together

$$\begin{bmatrix} a \\ b \end{bmatrix} + \begin{bmatrix} c \\ d \end{bmatrix} = \begin{bmatrix} a+c \\ b+d \end{bmatrix}$$

We define scalar multiplication by just multiplying every number in the column by the number

$$s\begin{bmatrix} a \\ b \end{bmatrix} = \begin{bmatrix} sa \\ sb \end{bmatrix}$$

## Properties of Vector Addition
Now vector addition has to obey some extra rules for it to be a vector space. 

Firstly, it has to be associative this means that

$$u + (v + w) = (u + v) + w$$

e.g. it doesn't matter what order we do the addition in

Secondly, it has to be commutative:

$$ u +  v = v + u$$

e.g. we can swap the order of the arguments

There must be a vector v such that for all vectors, w, in V we have

$$v + w = w$$

We call this v the zero vector and denote it 0. So we have

$$0 + w = w$$

Note that the zero vector is not the same as the 0 in the set of scalars

Finally, for every element v in the set of vectors, there is another vector w such that 

$$v + w = 0$$

We say w is the inverse of v and often write w as -v so we get

$$v + (- v) = 0$$

## Properties of scalar multiplication

Scalar multiplication also has to obey some extra rules.

Firstly, we must always have for every vector v:

$$1 * v = v$$

And then we must have

$$a*(b*v) = (a * b)v$$

What this means is that if we want to do scalar multiplication twice in a row we can just times the two scalars together first then multiply the vector by that

Finally, we have

$$(a + b)v = av + bv$$

## How scalar multiplication and vector addition interact
Finally, scalar multiplication and vector addition must interact in a certain way

$$a(u + v) = au + bv$$

## Summary
Now these rules might seem complicated but in fact, they are mostly the rules that we have for everyday addition and multiplication. They'll feel very natural after we do a bit more practice with them