---
layout: post
title: Basic Quantum Computing - Shor's Algorithm - Modular Exponentiation
author: Charles Thomas
---

In this series of posts, we're exploring a famous algorithm called Shor's Algorithm. 

In previous posts, we talked about using phase estimation to do order finding. In order to use phase estimation we need to be able to take a unitary operator U and construct a $$CU^n$$ gate that is a a gate that does 

$$CU^n \ket{j} \ket{s} = \ket{j}U^j\ket{s}$$ 

e.g. it runs U j times for an input j and doesn't change j. We can do this using a process called modular exponentiation which is what we're going to discuss in this post.

# Our Problem

Specifically, for us we have

$$U\ket{y} = \ket{(xy) \mod N}$$

So 

$$CU^n \ket{j} \ket{s} = \ket{j}\ket{(x^j s) \mod N}$$ 

We would like to do this efficiently. 

# A Helpful Observation

First, let's observe that

$$j = j_{t-1} 2^{t-1} + ... + j_0 2^0$$

where each $$j_i$$ is either 0 or 1. So 

$$x^j \mod N = x^{j_t 2^{t-1} + ... + j_0 2^0} \mod N= x^{j_t 2^{t-1}}*...*x^{j_0 2^0} \mod N$$

So the idea is we compute $$x^{2^n} \mod N$$ for n = $$0,...t-1$$

Then we multiply all the ones we need together to get $$x^j \mod N$$

Finally, we only have to multiply $$x^j \mod N$$ and $$s \mod N$$ together.

# Computing $$x^{2^n}$$

Now, we can compute $$x^{2^n} \mod N$$ for some n by repeatedly squaring. 

We compute $$x^2 \mod N$$ by squaring $$x\mod N$$.

Then we square $$x^2 \mod N$$ to get $$x^4 \mod N$$. 

And we keep repeating this until get  $$x^{2^n} \mod N$$.

This process of repeated squaring is known as modular exponentiation and allows us to compute $$x^j \mod N$$ easily.

