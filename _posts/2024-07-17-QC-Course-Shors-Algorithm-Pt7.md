---
layout: post
title: Basic Quantum Computing - Shor's Algorithm - Phase Estimation
author: Charles Thomas
---

In this series of posts, we're exploring a famous algorithm called Shor's Algorithm. In the last post, we talked about using phase estimation to do order finding. In this post, we're going to explore how phase estimation works.

# What problem does phase estimation solve?

Phase estimation solves the problem of given a unitary operator U and an eigenvector of it: 

$$\ket{u_s}$$ 

what is the eigenvalue of the state.

e.g. when we apply U to the eigenvector we get

$$U \ket{u_s} = e^{2\pi i \phi_s}\ket{u_s}$$

and phase estimation allows us to work out $$\phi_s$$

# Why can't we just measure the eigenvalue directly?

It would nice if we could just apply U to the eigenstate and then read off the eigenvalue, sadly U isn't necessarily Hermitian so we can't measure it directly.

# Phase Estimation - The Assumptions

Phase estimation starts by taking three inputs.

Firstly, it takes in a unitary operator U and an eigenvector of U whose eigenvalue we're going to estimate.

The third thing it needs is a $$CU^n$$ gate that is a a gate that does 

$$CU^n \ket{j} \ket{s} = \ket{j}U^j\ket{s}$$ 

e.g. it runs U j times for an input j and doesn't change j. This can be done by process called modular exponentiation. We will discuss this in a future post but for now we'll just assume we can do this.

# Step 1 - Setup

The first step is to setup the quantum state. We're going to start with n qubits all set to 0 and then our eigenvector u. This meas we have the state 

$$\ket{0}\ket{u}$$

# Step 2 - Create a superpostion

Next, we're going to create a superposition of the first n qubits. We'll do this by applying the Hadamard gate to each of them. 

So we get

$$H^{\otimes n}\ket{0} \ket{u} = \frac{1}{\sqrt{2^n}}\sum_{j=0}^{2^n -1} \ket{j}\ket{u}$$

# Step 3 - Apply the controlled U gates

We now have a bunch of states which look like

$$\ket{j}\ket{u}$$

where j is some integer

We want to apply U j times to each of them.

Thankfully, we can just use our 

$$CU^n$$

gate. So we get

$$\frac{1}{\sqrt{2^n}}\sum_{i=0}^{2^n -1} CU^n \ket{j}\ket{u}$$

$$=\frac{1}{\sqrt{2^n}}\sum_{i=0}^{2^n -1} \ket{j} U^j\ket{u}$$

Now since u is an eigenstate of U we get

$$=\frac{1}{\sqrt{2^n}}\sum_{i=0}^{2^n -1} \ket{j} (e^{2\pi i \phi_s})^j\ket{u}$$

$$=\frac{1}{\sqrt{2^n}}\sum_{i=0}^{2^n -1} \ket{j} e^{2\pi i \phi_s j}\ket{u}$$

# Step 4 - Inverse Fourier Transform
Now we're going to apply something called the Inverse Quantumm Fourier Transform (shorted to the inverse QFT). This is a super important part of quantum computing so we're going to give it its own post. So for now all we need to know if that it takes

$$\frac{1}{\sqrt{2^n}}\sum_{i=0}^{2^n -1} \ket{j} e^{2\pi i \phi_s j}\ket{u}$$

And sends it to

$$\ket{\tilde{\phi_s}}\ket{u}$$

Where $$\tilde{\phi_s}$$ is an n bit estimate for $$\phi_s$$

# Step 5 - Measure

After the inverse QFT we're left with the state

$$\ket{\tilde{\phi_s}}\ket{u}$$

So we just measure the first n qubits to get 

$$\tilde{\phi_s}$$

which is our estimation for $$\phi_s$$

# Why is it an estimate?
So how is our estimate 

$$\tilde{\phi_s}$$

different to 

$$\phi_s$$

Well $$\phi_s$$ can be any number, but we are only using n bits to represent it. This means that unless we're lucky and it fits in exactly n bits then our estimate will be slightly different to phi. You see this all the time in classical computers where some decimal numbers can't be nicely represented in a certain number of bits so the computer makes an approximation.

# Summary

So in summary we start with

$$\ket{0}\ket{u}$$

We then create a superposition to get

$$\frac{1}{\sqrt{2^n}}\sum_{j=0}^{2^n -1} \ket{j}\ket{u}$$

We then apply the controlled U gate to get

$$\frac{1}{\sqrt{2^n}}\sum_{i=0}^{2^n -1} \ket{j} e^{2\pi i \phi_s j}\ket{u}$$

Next, we apply the inverse QFT to get 

$$\ket{\tilde{\phi_s}}\ket{u}$$

which we can measure to get our estimate for $$\phi_s$$

