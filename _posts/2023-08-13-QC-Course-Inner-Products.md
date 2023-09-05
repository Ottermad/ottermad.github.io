---
layout: post
title: Basic Mathematics For Quantum Mechanics - Inner Products
author: Charles Thomas
---

## What is an inner product?
Last time, we talked about vector spaces and we said that they have two binary operations: vector addition and scalar multiplication.

We can add a third operation called an inner product to a vector space to turn it into an inner product space.

An inner product is a binary operation that takes in two vectors and gives us back a scalar. We usually represent it with a dot

$$\cdot : V \times V \rightarrow S$$

Or we write it with a set of angle brackets

$$\langle x, y \rangle$$


## Properties of an inner product

The inner product must obey 3 special properties

### Conjugate symmetry
What this means is if we reverse the order of an inner product, we just get the complex conjugate of the original out. So

$$\langle x, y \rangle = \overline{\langle y, x \rangle}$$

In this case where the set of scalars we are working with is the real numbers, then since 

$$x = \overline{x}$$

We get  

$$\langle x, y \rangle = \langle y, x \rangle$$

### Linearity in the first argument
Linearity in the first argument means two things. Firstly if x, y and z are all vectors then

$$\langle x + y, x \rangle = \langle x, z \rangle + \langle y, z \rangle$$

Secondly, if s is a scalar and x and y are vectors then

$$\langle sx, y \rangle = s\langle x, y \rangle$$

### Positive-definiteness 
This just means that the inner product of a vector with itself is always greater than or equal to 0

$$\langle x, x \rangle \geq 0$$

## Size of vectors
An inner product is often said to give geometry to a space. This is because it allows us to talk about the sizes of vectors and the angles between them.

We can denote the size of the a vector v as \|v\| and we use the following the formula:

$$|v| = \sqrt{\langle v, v \rangle}$$


## Angle between two vectors
If we have two vectors x and y then the angle t between them is defined as:

$$cos(t) = \frac{\langle x, y \rangle}{|x||y|} = \frac{\langle x, y \rangle}{\sqrt{\langle x, x \rangle}\sqrt{\langle y, y \rangle}}$$ 


## Dot product from school
In school, you might have encounter the dot product. The dot product is an example of inner product.

Consider the vector