---
layout: post
title: Basic Mathematics For Quantum Mechanics - Eigenvectors
author: Charles Thomas
---

Let's consider a matrix A and a vector v. When we multiply when together we get back another vector w. So 

$$Av = w$$

Normally w is completely different to v. However, sometimes w is multiple of v. What I mean by this is that there is some scalar, s, that when I times v by it I get w. So

$$w = sv$$

For example

$$\begin{bmatrix}4 \\ 2\end{bmatrix} = 2\begin{bmatrix}2 \\ 1\end{bmatrix}$$

In the cases where w is a scalar multiple of v we get:

$$Av = sv$$

And we call v an eigenvector of A with eigenvalue s

Let's look at an example. Consider

$$A = \begin{bmatrix}-5 & 2 \\ -9 & 6\end{bmatrix}$$

$$v = \begin{bmatrix}1 \\ 1\end{bmatrix}$$

$$Av = \begin{bmatrix}-3 \\ -3\end{bmatrix} = -3\begin{bmatrix}1 \\ 1\end{bmatrix}$$

So v is an eigenvector of A with eigenvalue -3

Eigenvectors and values are extremely useful in all sorts of scenarios but this is all we need to know for now.