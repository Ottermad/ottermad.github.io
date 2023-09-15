---
layout: post
title: Basic Mathematics For Quantum Mechanics - Linear Maps
author: Charles Thomas
---

## What is a linear map?

Let f be a map between two vector spaces

If 

$$f(av + bw) = f(av) + f(bw)$$

where v,w are vectors and a and b are scalars then f is a linear map

## Linear maps are completely determined by its action on the basis

Let f be a linear map

Let V have the following basis

$$\{b_1, b_2, ...., b_n\}$$

Then we can write any vector, v as:

$$\sum_i^n a_i b_i$$

Now, let's try applying f to v

$$f(v) = f(\sum_i^n a_i b_i)$$

$$= \sum_i^nf( a_i b_i)$$

$$= \sum_i^na_i f(b_i)$$

So if we know what f does to each basis vector, then we know what it does to any vector.

Let's write f in the following way:

$$[f(b_1) f(b_2) f(b_3) ... f(b_n)]$$

Here's an example

$$[f(b_1) f(b_2)] = [3 5]$$

So 

$$f(4b_1 + 6b_2) = 4*3 + 6*5 = 42$$


## Linear maps that return vectors

In our example above, the linear maps only gave us back a number. But they can also give us back vectors.

So consider

$$f(b_1) = \begin{bmatrix}3 \\ 4\end{bmatrix}$$

$$f(b_2) = \begin{bmatrix}7 \\ 2\end{bmatrix}$$

So we get

$$f(b_1 + 3b_2) = \begin{bmatrix}3 \\ 4\end{bmatrix} + 3*\begin{bmatrix}7 \\ 2\end{bmatrix} = \begin{bmatrix}24 \\ 10\end{bmatrix}$$

So we can write f using a similar syntax to the above and we get

$$[f(b_1) f(b_2)] = [\begin{bmatrix}3 \\ 4\end{bmatrix} \begin{bmatrix}7 \\ 2\end{bmatrix}]$$

But we will drop the inner sets of brackets to make it more readable so we get

$$=\begin{bmatrix} 3 & 7 \\ 4 & 2\end{bmatrix}$$

This is exactly what we have called a matrix. This means that every matrix is actually just describing a linear map.

If we have a matrix A then we write Av to represent passing the vector v to matrix A. So

$$f(v) = Av$$

In the example above we used 

$$v = b_1 + 3b_2$$

So we could write

$$f(b_1 + 3b_2) = \begin{bmatrix} 3 & 7 \\ 4 & 2\end{bmatrix}(b_1 + 3b_2)$$ 

Using the syntax for column vectors from a previous post we get

$$= \begin{bmatrix} 3 & 7 \\ 4 & 2\end{bmatrix}\begin{bmatrix} 1 \\ 3\end{bmatrix} = \begin{bmatrix}24 \\ 10\end{bmatrix}$$

## Matrices as linear maps
We've just seen that linear maps correspond to matrices. Where the ith column tells us what happens to the ith basis vector under the map.

While this is true, there is one caveat. Vector spaces can have more than one basis. So when we write a linear map as a matrix we have chosen a specific basis to use. If we change the basis then the linear map will be represented by a different basis.


## Matrix dimensions
Thinking about matrices as linear maps tells us about which sizes of matrices can be multiplied by which vectors.

If a matrix is a linear map from an n-dimension space, then that space has n basis vectors, so the matrix must have n columns, one for each basis vector.

So an m x n matrix must act on n-dimensional vectors because it is a map from an n-dimensional space

The number of rows, m, tells us the dimension of the output space.

## Matrix multiplication as working on multiple vectors at once

While matrix multiplication can at first seem rather arbitrary, there are actually a couple of nice ways of thinking about it.

The first is to consider it as a shortcut for acting on many vectors at once.

So if I have a matrix A and two vectors v and w. If I want to work out Av and Aw I might do

$$v' = Av$$

$$w' = Aw$$

But I can write this as one operation by defining the matrix B where the first column of B is v and the second column of B is w.

Then the matrix multiplication AB will give a matrix where the first column is the result of Av and the second column is the result of Aw


Let's take a look at an example:

$$A = \begin{bmatrix}1& 3 \\ 7 & 5\end{bmatrix}$$

$$v = \begin{bmatrix}2 \\ 6\end{bmatrix}$$

$$w = \begin{bmatrix}4 \\ 3\end{bmatrix}$$

So we know that:

$$Av = \begin{bmatrix}20 \\ 44\end{bmatrix}$$

$$Aw = \begin{bmatrix}13 \\ 43\end{bmatrix}$$


So

$$\begin{bmatrix}1& 3 \\ 7 & 5\end{bmatrix}\begin{bmatrix}2 & 4 \\ 6 & 3\end{bmatrix} = \begin{bmatrix}20 & 13 \\ 44 & 43\end{bmatrix}$$

Since matrix multiplication can be thought of as acting on as many n-dimensional vectors. This tells us that an m x n matrix must act on an n x p matrix because each column in the second matrix represents an n-dimensional vector.


## Matrix multiplication as the composition of linear maps
There is another way of thinking about matrix multiplication. 

If I have a linear map f from X to Y and another linear map g from Y to Z then I can compose the two maps together.

This means I apply the map f and then the map g.

So I can define a new map 

$$h : X \to Z$$

$$h(v) = g(f(v))$$

Given we know there is a matrix that represents f and a matrix that represents g is there a way we can use these two matrices to work out the matrix representing h is. Well, we can just multiply them together.

Seeing this is a little complicated but we'll work through it step by step.

Let's assume f goes from an m-dimensional space to an n-dimensional space. So its matrix will need m columns - one for each dimension of the input space and n rows - one for each dimension of the output space.


$$F = \begin{bmatrix}
 f_{11} & f_{12} & ... & f_{1m} \\ 
 f_{21}  & f_{22} & ... & f_{2m} \\
  .... \\
  f_{n1} & f_{n2} & ... & f_{nm}
\end{bmatrix}$$

Now since g takes in the output from f it must go from an n-dimensional space but then it can go to any dimensional space so let's just say it is a p-dimensional space. So g will have n columns and p rows.

$$G = \begin{bmatrix}
 g_{11} & g_{12} & ... & g_{1n} \\ 
 g_{21}  & g_{22} & ... & g_{2n} \\
  .... \\
  g_{p1} & g_{p2} & ... & g_{pn}
\end{bmatrix}$$


If 

$$h = g \circ f$$

Then we should have

$$Hv = G(Fv)$$

To work out what H is let's pick the ith basis vector for our m dimension space and call it 

$$b_i$$

If we can work out what H should do to this basis vector then we'll know what the ith column of H should be

When f acts on it we get back the ith column

$$Fb_i = \begin{bmatrix}f_{1i} \\ ... \\ f_{ni}\end{bmatrix}$$

Now let's act on this with G

$$GFb_i = G\begin{bmatrix}f_{1i} \\ ... \\ f_{ni}\end{bmatrix}$$

This is just a matrix acting on a vector so we can work out what this is:

$$ = f_{1i}\begin{bmatrix}
 g_{11} \\ 
 g_{21} \\
  .... \\
  g_{p1}
\end{bmatrix} 

+ .... + 

f_{ni}\begin{bmatrix}
 g_{1n} \\ 
 g_{2n} \\
  .... \\
  g_{pn}
\end{bmatrix}$$

$$ = \begin{bmatrix}
 f_{1i}g_{11} + ... + f_{ni}g_{1n}\\ 
 f_{1i}g_{21} + ... + f_{ni}g_{2n} \\
  .... \\
  f_{1i}g_{p1} + ... + f_{ni}g_{pn}
\end{bmatrix} 
$$

So this tells us how to work out the ith column of H which is in fact the same as the rule I gave you in the previous post
