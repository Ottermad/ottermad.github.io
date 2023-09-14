---
layout: post
title: Basic Mathematics For Quantum Mechanics - Matrices
author: Charles Thomas
---

In this post, we're going to explore what matrices are and the rules for working with them. For now, these rules might seem a bit arbitrary but we'll see in a later post that they actually come from a really interesting place.

## Matrices as grids of numbers
A matrix is just a grid of numbers. Let's take a look at one:

$$\begin{bmatrix}2 & 7 & 3 \\4 & 6 & 1\end{bmatrix}$$

This matrix has 2 rows and 3 columns so we say it is a 2 x 3 matrix. In general, a matrix can have m rows and n columns and is called an m x n matrix
 
## Adding matrices
If we take two matrices of the same size, then we can add them together. We do this by adding each of the components together. So 

$$\begin{bmatrix}2 & 7 & 3 \\4 & 6 & 1\end{bmatrix} + \begin{bmatrix}5 & 13 & 2 \\1 & 9 & 12\end{bmatrix} = \begin{bmatrix}2+5 & 7+13 & 3+2 \\4+1 & 6+9 & 1+12\end{bmatrix}$$ 

$$=\begin{bmatrix}7 & 20 & 5 \\5 & 15 & 13\end{bmatrix}$$

## Multiplying matrices by a scalar
Given a scalar, we can also multiply it by a matrix by multiplying every component of the matrix by it. For example,

$$2\begin{bmatrix}2 & 7 & 3 \\4 & 6 & 1\end{bmatrix} = \begin{bmatrix}4 & 14 & 7 \\8 & 12 & 2\end{bmatrix}$$

## Multiplying two matrices together 
We can also multiply two matrices but the rule for this seems a bit weird. The first thing we have to know about multiplying matrices is that it is non-commutative. What this means is that if I have two matrices A and B then AB is not the same as BA.

Next, we have to know that we can only multiply two matrices together if the first matrix has the same number of columns and the second column has rows. So if we have two matrices A and B and we want to work out AB. Then if A has p columns, b must have p rows.

Now we can actually get to the rule for multiplying matrices. If I have two matrices A and B then the number in the ith row and j th column is given by the dot product of the ith row of A and the jth column of B. Let's do an example


$$A = \begin{bmatrix}2 & 7 & 3 \\4 & 6 & 1\end{bmatrix}$$

$$B = \begin{bmatrix}5 & 9 \\3 & 1 \\ 2 & 1\end{bmatrix}$$

Then the number in the first row and first column is:

$$\begin{bmatrix}2 & 7 & 3 \end{bmatrix}\cdot \begin{bmatrix}5 \\3 \\ 2 \end{bmatrix} = 10 + 21 + 6 = 37$$

And in the first row and second column, we get: 

$$\begin{bmatrix}2 & 7 & 3 \end{bmatrix}\cdot \begin{bmatrix}9 \\1 \\ 1 \end{bmatrix} = 18 + 7 + 3 = 28$$


Repeating this for the second row we get:


$$AB = \begin{bmatrix}\
37 & 28 \\
40 & 43
\end{bmatrix}$$

## Identity matrix
There is a special matrix called I that when you multiply another matrix by it the matrix doesn't change. So for all matrices A we have

$$AI = A$

This matrix I is also called the identity matrix and it is the matrix with 1s along its diagonal and 0s everywhere else.

So for example the 2 x 2 identity matrix is

$$\begin{bmatrix}1 & 0 \\ 0 & 1\end{bmatrix}$$

## Inverse matrices
Finally, we need to talk about inverse matrices. If I have two matrices A and B and when you multiply them together you get the identity matrix then we say B is the inverse of A and we denote it by

$$B = A^{-1}$$

We call it the inverse because if I have a matrix C and multiply by A and then multiply it B then B undoes A. 

$$CAB = CAA^{-1} = CI = C$$
