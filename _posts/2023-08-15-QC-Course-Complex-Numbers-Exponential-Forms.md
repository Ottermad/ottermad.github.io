---
layout: post
title: Basic Mathematics For Quantum Mechanics - Exponential Form of Complex Numbers
author: Charles Thomas
---

## Polar Form

Last time, we talked about complex numbers as numbers of the form a + bi where i is the square root of -1. This is true but there is another way of writing them which is sometimes more helpful.

Let's start by recalling the argand diagram where we plot the real part of the x axis and the imaginary part on the y axis.

![Argand Diagram](/assets/exponentialform/argand.png)

Here the complex number is represented by an arrow. You might remember from school that there is anoter way of describing this arrow.

We can describe an arrow by how long it and what angle it makes to the positive x axis. The length of the arrow is shown in the picture by the letter r and the angle is denoted by the letter t

![Polar Form](/assets/exponentialform/polar.png)

So we can write a complex number as a pair of numbers (r, t) where r is the length and t is the angle.

r and t have special names. r is called the modulus of the complex number and t is called the argument. 

Given a complex number in polar form so we have a radius and an angle we can use a bit of high school trigonmetry to find that:

$$a = r cos(t)$$

$$b = rsin(t)$$

So putting this together we can write a complex number as 

$$rcos(t) + irsin(t) = r(cos(t) + i sin(t))$$

## Euler's Formula
One of the most famous formulas in mathematics is that

$$e^{it} = cos(t) + isin(t)$$

This identity is called Euler's formula and using it we can any complex number in the following form

$$r(cos(t) + i sin(t)) = re^{it}$$

This is a really helpful form to write a complex number in as it makes it easy to see what the modulus is which is often important in Quantum Computing.

It also makes multiplying two complex numbers really easy as:

$$r_1e^{it_1} * r_2e^{it_2} = r_1r_2^{i(t_1+t_2)}$$

The other thing it makes easy is taking the complex conjugate

$$\overline{re^{it}} = re^{-it}$$