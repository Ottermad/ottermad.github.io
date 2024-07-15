---
layout: post
title: Basic Quantum Computing - Shor's Algorithm - Order Finding Using Phase Estimation
author: Charles Thomas
---

In this series of posts, we're exploring a famous algorithm called Shor's Algorithm. In this post, we're going to look at how we do order finding on a quantum computer using something called phase estimation.

# Order Finding: A reminder

Let's start with a reminder of what the problem of order finding is. Given a two numbers x and N what is the smallest integer $$r > 1$$ so that 

$$x^r \mod N = 1$$

This smallest r is called the order and we want to find it.

# What is phase estimation?
To do order finding we'll make use of another quantum algorithm: phase estimation. Phase estimation allows us to take a unitary operator U and an eigenvector of it: 

$$\ket{u_s}$$ 

and to estimate the eigenvalues.

This means given 

$$U \ket{u_s} = e^{2\pi i \phi_s}\ket{u_s}$$

we can can work out $$\phi_s$$

(Note that the eigenvectors of unitary operators are always of unit modulus hence we can write it in the above form)

But how does this help us do order finding?

# Using Phase Estimation to do order finding

To see how it helps, let's fix x and N and we want to find r (the order).


Now if we have a unitary operator $$U$$ such that

$$U\ket{y} = \ket{(xy) \mod N}$$

Then this has eigenstates given by 

$$\ket{u_s} = \frac{1}{\sqrt{r}}\sum_{k=0}^{r-1}exp(\frac{-2\pi i sk}{r})\ket{x^k \mod N}$$ 

with eigenvalue 

$$exp(\frac{2\pi i s}{r})$$ 

where $$0 \leq s < r - 1$$

This is because

$$U\ket{u_s} = exp(\frac{2\pi i s}{r})\ket{u_s}$$

So we if we can apply phase estimation we can estimate $$s/r$$ we'll denote our estimation as $$\tilde{s/r}$$

Then from our approximation for $$s/r$$ we can work out r using the classical continued fractions algorithm (which we'll explain in a future post)

# Making Eigenstates
In order to use phase estimation we need to be able to make our eigenstate

$$\ket{u_s}$$ 

but do this we need to r which exactly the thing we want to 

find. So what are we to do?

We'll we can be sneaky and notice that 

$$\frac{1}{\sqrt{r}}\sum_{s=0}^{r-1} \ket{u_s} = \ket{1}$$

So as long as we prepare the state $$\ket{1}$$ which we can do easily then we can act on that. This will calculate a superposition of the estimates for all s so we can measure the state and we will get an estimate for $$s/r$$ for some s. We just won't know which one. This is fine as the continued fractions algorithm doesn't require us to know s.

# Summary

So putting this all together we start with the state

$$\ket{0}\ket{1}$$

We can rewrite this as

$$\ket{0}\frac{1}{\sqrt{r}}\sum_{s=0}^{r-1} \ket{u_s} = \frac{1}{\sqrt{r}}\sum_{s=0}^{r-1} \ket{0}\ket{u_s}$$

We can apply phase estimation to get

$$\frac{1}{\sqrt{r}}\sum_{s=0}^{r-1} \ket{\tilde{s/r}} \ket{u_s}$$

We do a measurement so we get

$$\ket{\tilde{s/r}}\ket{u_s}$$ 

for some unknown s

We can then apply the continued fractions algorithm to work out r