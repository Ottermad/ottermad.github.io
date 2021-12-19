---
layout: post
title: Basics Maths For Quantum Mechanics
author: Charles Thomas
---


# Mathematical interlude

## Complex Numbers
A complex number is a number that is written as $$a + bi$$. Where a and b are real numbers (the ones we usually think of when we think about numbers) and $$i$$ is the square root of -1. Some examples of these are $$2 + 3i$$ or $$4 + 7i$$

We can do an operation called complex conjugation where we swap the sign of b: so $$a + bi$$ becomes $$a - bi$$. For example, the complex conjugate of $$3 + 4i$$ is $$3 - 4i$$. For a complex number z we will often call its complex conjugate $$z^*$$

We can two complex numbers together by adding the two parts of the numbers separately. So $$(a + bi) + (c + di) = (a+c) + (b+d)i$$ 
An example of this is: $$(2 + 3i) + (7 + 10i) = 9 + 13i$$  

We can also multiply complex numbers together using this formula: $$(a + bi)(c + di) = (ac - bd) + (bc + ad)i$$. To see why this works let's look at an example: $$(3 + 4i)(5 + 6i) = 3(5 + 6i) + 4i(5+ 6i) = 15 + 18i + 20i + 24i^2 = 15 + 38i  -24 = -9 + 38i$$

## Vectors
You can think of vectors as a list of numbers: $$\begin{bmatrix}3 \\ 7 \\ 2 + 4i\end{bmatrix}$$

If we have two vectors, a and b, we can calculate the inner product between them. We can do this by taking the first element of a, taking its complex conjugate then multiplying by the first element of b. We repeat this for all the elements in a. Finally we add all the numbers we go from doing this together. We can write this mathematically as $$\sum{a_i^*b_i}$$

In school, you may have encounter something very similar called the dot product. That is the version of the inner product that works if do not have complex numbers.

## Matrices
A matrix is a m by n x grid of numbers. For example: $$\begin{bmatrix}2 & 3 \\ 4 & 5\end{bmatrix}$$

* Multiplication
We can multiply two matrices to give another matrix

* Identity

* Inverse

We can do an operation called the transpose where the rows become columns and the columns become rows.  For example if we have the matrix $$\begin{bmatrix}2 & 3 \\ 4 & 5\end{bmatrix}$$ its transpose is $$\begin{bmatrix}2 & 4 \\ 3 & 5\end{bmatrix}$$

* Conjugate transpose