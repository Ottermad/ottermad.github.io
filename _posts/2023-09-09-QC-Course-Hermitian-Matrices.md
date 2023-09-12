---
layout: post
title: Basic Mathematics For Quantum Computing - Hermitian Matrices
author: Charles Thomas
---

In this post, we're going to be dicussing what Hermitian matrices are.

## Transpose of a matrix
Let's start by learning about the transpose of a matrix. A tranpose pose of a matrix is just flipping the matrix so that every row becomes a column and visversa.

For example if I have

$$A = \begin{bmatrix}-5 & 2 \\ -9 & 6\end{bmatrix}$$

Then the transpose is:

$$\begin{bmatrix}-5 & -9 \\ 2 & 6\end{bmatrix}$$

We denote the transpose by writing of a matrix A by writing:

$$A^T$$

If a matrix is its own tranpose we may that the matrix is symmetric

## Conjugate transpose of a matrix
If the numbers in a matrix are complex we can also consider the cojugate transpose of the matrix. All this means is that we replace every element by it's complex conjugate and then take the tranpose.

So if

$$A = \begin{bmatrix}-5 + 2i & 2+3i \\7+2i & 3\end{bmatrix}$$

Then the conjugate transpose is 

$$\begin{bmatrix}-5 - 2i & 7-2i \\ 2 - 3i & 3\end{bmatrix}$$

And we denote this by 

$$A^\dagger$$

## Hermitian matrices
Now we can define Hermtian matrices. A Hermitian matrix is simply one that is equal to its own complex conjugate so we have:

$$A = A^\dagger$$

For example:

$$\begin{bmatrix}1 & 2+3i \\2-3i & 3\end{bmatrix}$$

is a Hermitian matrix as it is equal to its conjugate tranpose.


## Unitary matrices
Finally, we can talk about unitary matrices. A matrix A is unitary if its inverse is it's conjugate tranposes.

So we get

$$AA^\dagger = I$$

For example if

$$A = \begin{bmatrix}\frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}}  \\\frac{1}{\sqrt{2}}i & -\frac{1}{\sqrt{2}} i\end{bmatrix}$$

Then

$$A^\dagger = \begin{bmatrix}\frac{1}{\sqrt{2}} & -\frac{1}{\sqrt{2}}i  \\\frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} i\end{bmatrix}$$

So we get

$$AA^\dagger = I$$