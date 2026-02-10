---
layout: post
title: Basic Quantum Computing - Shor's Algorithm - Quantum Fourier Transform
author: Charles Thomas
---

In this series of posts, we're exploring a famous algorithm called Shor's Algorithm. In the previous post, explored how phase estimation work and in doing so we mentioned the Quantum Fourier Transform but we didn't dive into it. In this post we will but before we jump to the Quantum Fourier Transform, let's talk about its classical analogue: the discrete Fourier transform.

# The Discrete Fourier Transform
Let's start with a list of k numbers: 

$$[x_0, x_1, ..., x_k]$$

Then we define a new list of numbers:

$$[y_0, y_1, ..., y_k]$$

where 

$$y_a = \frac{1}{\sqrt{k}}\sum_{j=0}^{k-1} x_j e^{2\pi ija/k}$$

## Example

# The Quantum Fourier Transform
Now let's go to the Quantum version.

In the Quantum version we start with n qubits

$$\ket{q_1}....\ket{q_n}$$

Let's assume they're in some state in the computational basis. This means each has the form of

$$\ket{a}$$

where 

$$0 \leq a < 2^n - 1$$

Then the Quantum Fourier Transform (QFT) sends a to 

$$\ket{a} \to \frac{1}{\sqrt{2^n}}\sum_{j=0}^{2^n-1} \ket{j} e^{2\pi ija/2^n}$$

Now if our state was not a basis state, we can express it in terms of a basis then apply this transformation to each basis state and add them together.

## Example

# An important rewriting
There is one important way of rewriting the Fourier transform called the product representation. It is really important as it makes it much easier to construct the circuit to implement to the QFT.

If we have our n qubit basis state:

$$\ket{a}$$

then we write it out as 

$$\ket{a_1 a_2 ... a_n}

where each $$a_i$$ is 0 or 1

Then we can applying the QFT does the following

$$\ket{a} \to \frac{()}{2^{n/2}}$$
