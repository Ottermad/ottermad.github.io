---
layout: post
title: Basics Maths For Quantum Mechanics
author: Charles Thomas
---

I originally intended to write a blog post on the No Cloning Theorem. But as I was writing it I realised in order to make it accessible I need a mathematical primer that I could point people to. So that is what this is: the bare minimum of maths needed to understand basic quantum mechanics.


# Complex Numbers
A complex number is a number that is written as $$a + bi$$. Where a and b are real numbers (the ones we usually think of when we think about numbers) and $$i$$ is the square root of -1. Some examples of these are $$2 + 3i$$ or $$4 + 7i$$

## Addition
We can two complex numbers together by adding the two parts of the numbers separately. So $$(a + bi) + (c + di) = (a+c) + (b+d)i$$ 
An example of this is: $$(2 + 3i) + (7 + 10i) = 9 + 13i$$  

## Multiplication
We can also multiply complex numbers together using this formula: 

$$(a + bi)(c + di) = (ac - bd) + (bc + ad)i$$. 

To see why this works let's look at an example: 

$$(3 + 4i)(5 + 6i) $$

$$= 3(5 + 6i) + 4i(5+ 6i) $$

$$= 15 + 18i + 20i + 24i^2 $$

$$= 15 + 38i  -24 $$

$$= -9 + 38i$$

## Complex Conjugation
We can do an operation called complex conjugation where we swap the sign of b: so $$a + bi$$ becomes $$a - bi$$. For example, the complex conjugate of $$3 + 4i$$ is $$3 - 4i$$. For a complex number z we will often call its complex conjugate $$z^*$$

# Vectors
You can think of vectors as a list of numbers: $$\begin{bmatrix}3 + 4i \\ 5 \\ 2\end{bmatrix}$$

## Addition
If two vectors have the same number of elements then we can add them together. We do this by adding each element individually. 

$$\begin{bmatrix}3 \\ 7 \\ 2 + 4i\end{bmatrix} + \begin{bmatrix}3 + 4i \\ 5 \\ 2\end{bmatrix} = \begin{bmatrix}6 + 4i \\ 12 \\ 4 + 4i\end{bmatrix}$$

## Scalar multiplication
We can a vector bigger or smaller by multiplying it by a number. To do this you just multiply each element of the vector by the number. For example:

$$4\begin{bmatrix}3 + 4i \\ 5 \\ 2\end{bmatrix} = \begin{bmatrix}12 + 16i \\ 20 \\ 8\end{bmatrix}$$

## Dot product
If we have two vectors of the same size, a and b, we can also work out the dot product between them. This is often represented by the symbol $$\cdot$$.  We can do this by taking the first element of a and multiplying by the first element of b. We do for this for all the elements then add the answers together. For example:

$$\begin{bmatrix}3 \\ 8 \\ 1\end{bmatrix} \cdot \begin{bmatrix}7 \\ 2 \\ 9\end{bmatrix} = 3 \times 7 + 8 \times 2 + 1 \times 9 = 21 + 16 + 9 = 46$$

## Inner products
If we have two vectors, a and b, we can calculate the inner product between them. We can do this by taking the first element of a, taking its complex conjugate then multiplying by the first element of b. We repeat this for all the elements in a. Finally we add all the numbers we got together. We can write this mathematically as $$\sum{a_i^*b_i}$$

Let's work out the inner product between $$\begin{bmatrix}3 + 4i \\ 5 \\ 2\end{bmatrix}$$ and $$\begin{bmatrix}3 \\ 7 \\ 2 + 4i\end{bmatrix}$$ as an example. 

The inner product is:

$$(3+4i)^* \times 3 + 5 \times 7 + 2 \times (2 + 4i)$$

$$= (3-4i) \times 3 + 5 \times 7 + 2 \times (2 + 4i)$$

$$= 9 -12i + 35 + 4 + 8i = 48 - 4i$$

# Matrices
A matrix is a grid of numbers. For example: $$\begin{bmatrix}2 & 3 \\ 4 & 5\end{bmatrix}$$. We describe the size of a matrix by the number of rows and columns it has. A matrix with m rows and n columns is called a m by n matrix.

If a matrix has the same number of rows and columns it is called a square matrix.

## Multiplication
We can multiply two matrices to give another matrix. We can only do this is if the size of the matrices are right. This means to multiply matrices A and B to get AB the number of columns of A must be the same of the number of rows of B.
The output of this multiplication will be matrix with the same number of rows as A and the same number of columns as B. This means multiplying an m x n matrix with an n x p matrix gives you an m x p matrix.    

To multiply matrices A and B together to get AB, you do each number of the number separately. To work out the number in the ith row and jth column of AB you take the ith row of A and the jth column of B and take the dot product between them. 

$$\begin{bmatrix}2 & 3 \\ 4 & 5\end{bmatrix}\begin{bmatrix}1 & 7 \\ 11 & 9\end{bmatrix} = \begin{bmatrix}
\begin{bmatrix}2 \\ 3\end{bmatrix} \cdot \begin{bmatrix}1 \\ 11\end{bmatrix} & \begin{bmatrix}2 \\ 3\end{bmatrix} \cdot \begin{bmatrix}7 \\ 9\end{bmatrix} \\
\begin{bmatrix}4 \\ 5\end{bmatrix} \cdot \begin{bmatrix}1 \\ 11\end{bmatrix} & \begin{bmatrix}4 \\ 5\end{bmatrix} \cdot \begin{bmatrix}7 \\ 9\end{bmatrix} 
\end{bmatrix}
=\begin{bmatrix}35 & 41 \\ 59 & 73\end{bmatrix}
$$

It is important to note that matrix multiplication is not commutative. This means $$AB \neq BA$$ 

## Identity
There is a special matrix called the Identity matrix. When you multiply a matrix, M, by it, you get M back. It's the equivalent of multiplying by 1.

$$MI = IM = M$$ 

## Inverses
If we have two matrices, A and B, and we multiply them together. If the result is the identity matrix then we call B the inverse matrix of A and write it as $$A^{-1}$$

## Transpose
We can do an operation called the transpose where the rows become columns and the columns become rows.  For example if we have the matrix $$\begin{bmatrix}2 & 3 \\ 4 & 5\end{bmatrix}$$ its transpose is $$\begin{bmatrix}2 & 4 \\ 3 & 5\end{bmatrix}$$

## Conjugate transpose
There is another operation called the conjugate tranpose which is where we tranpose the matrix and take the complex conjugate of all the entries. 

So  $$\begin{bmatrix}2 + 7i & 3 \\ 4 + 5i  & 5\end{bmatrix}$$ becomes  $$\begin{bmatrix}2 -7i & 4 - 5i  \\ 3 & 5\end{bmatrix}$$

For a matrix M, its conjugate transpose is often denoted $$M^\dagger$$