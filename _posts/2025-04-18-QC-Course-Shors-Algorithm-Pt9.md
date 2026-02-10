---
layout: post
title: Basic Quantum Computing - Shor's Algorithm - Modular Exponentiation
author: Charles Thomas
---

In this series of posts, we're exploring a famous algorithm called Shor's Algorithm. In previous posts, we talked about using phase estimation to do order finding. In order to use phase estimation we need to be able to take a unitary operator U and construct a $$CU^j$$ gate that is a a gate that does 

$$CU^j \ket{j} \ket{s} = \ket{j}U^j\ket{s}$$ 

e.g. it runs U j times for an input j and doesn't change j. We can do this using a process called modular exponentiation which is what we're going to discuss in this post.
