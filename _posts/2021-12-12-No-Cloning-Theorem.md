---
layout: post
title: No Cloning Theorem
author: Charles Thomas
---

In normal computers we can copy the state of a bit. For instance, we use checkpointing to preserve the state of the system in case something happens to it.

We cannot do this in Quantum computing. This causes problems as it means we have to start the whole program again from the start if something goes wrong.

To understand why we first we need to understand a bit of quantum mechanics.

# Quantum Mechanics Intro

## Representing States
A qubit is represented by a vector $$\begin{bmatrix}a \\ b\end{bmatrix}$$ where $$a^2 + b^2 = 1$$ and a & b are complex numbers.

Multiple qubit systems are represented by the ‘kronecker product’ ($$\otimes$$) of the vectors so a system of two qubits:  $$\begin{bmatrix}a \\b \end{bmatrix}$$ and $$\begin{bmatrix}c \\ d\end{bmatrix}$$ represented as  $$\begin{bmatrix}a \\b \end{bmatrix} \otimes \begin{bmatrix}c \\ d\end{bmatrix}$$ which gives us the vector:  $$\begin{bmatrix}ac \\ ad \\ bc \\ bd\end{bmatrix}$$

## Measurements
There are two kinds of operations in quantum mechanics. The first is a measurement. These take a quantum state and put it in a definite state. This means it takes from being any vector and puts it into one of a certain number of states. 

For example a measurement might take a qubit and put it into either   $$\begin{bmatrix}1 \\ 0\end{bmatrix}$$ or  $$\begin{bmatrix}0 \\ 1\end{bmatrix}$$.

Since measurements reduce any vector to be one of a fixed number of vectors we cannot use measurements to clone any arbitrary state.

## Evolution
Quantum systems evolve  (change with time) according to unitary transformations. For our purpose we can think of our vector, v, being multiplied by some matrix U to give a new vector which is the state of the system later on in time.

The matrix U has to unitary what that means that its inverse is the same as its conjugate transpose. These matrices have the special property that they preserve inner products.

### Proof that unitary matrices preserve inner products
Let $$Uv = a$$ and $$Uw = b$$

The inner product of v and w is $$(v, w) = \sum_i{v_i^*w_i}$$

The inner product of a and b is $$(a, b) = \sum_i{a_i^*b_i} = \sum_i{(Uv)_i^*(Uw)_i}$$


# Proof of no cloning
We can do a proof by contradiction by assuming we have some copying transform C. We know that C is unitary.

Initially have two vectors $$\begin{bmatrix}a \\b\end{bmatrix}$$ and $$\begin{bmatrix}c \\d\end{bmatrix}$$ so have combined state vector $$\begin{bmatrix}ac \\ ad \\ bc \\ bd\end{bmatrix}$$

C acts on  $$\begin{bmatrix}ac \\ ad \\ bc \\ bd\end{bmatrix}$$ to give$$\begin{bmatrix}aa \\ ab \\ ab \\ bb\end{bmatrix}$$

Now imagine we do the process again with   $$\begin{bmatrix}e \\f\end{bmatrix}$$ and $$\begin{bmatrix}c \\d\end{bmatrix}$$ so
$$C \begin{bmatrix}ec \\ ed \\ fc \\ fd\end{bmatrix}$$ becomes $$\begin{bmatrix}ee \\ ef \\ ef \\ ff\end{bmatrix}$$

Now take the inner product before we did the cloning  $$(\begin{bmatrix}ac \\ ad \\ bc \\ bd\end{bmatrix}, \begin{bmatrix}ec \\ ed \\ fc \\ fd\end{bmatrix}) 
= (ac)^* (ec) + (ad)^* (ed) + (bc)^* (fc) + (bd)^* (fd) 
= a^* e(cc^* + dd^*) + d^*f (cc^* + dd^*) 
= a^* e + d^*f$$


Now if we take the inner products after the cloning we get:

$$(\begin{bmatrix}aa \\ ab \\ ab \\ bb\end{bmatrix}, \begin{bmatrix}ee \\ ef \\ ef \\ ff\end{bmatrix} 
= a^* a^* ee + a^* b^* ef + a^* b^* ef + b^* b^* ff 
= (a^* e)^2 + 2(a^* b^* ef) + (b^* f)^2
= (a^* e + b^* f)^2 
$$

Since C preserves inner products we have $$a^* e + d^*f = (a^* e + b^* f)^2 $$. The only solutions to this are:
$$(a^* e + b^* f) = 0$$ or $$(a^* e + b^* f) = 1$$ 

But this means  $$\begin{bmatrix}a \\b\end{bmatrix}$$ and  $$\begin{bmatrix}e \\f\end{bmatrix}$$ cannot be any two vectors which is a contradiction.

Therefore there cannot exist a way of cloning arbitrary quantum states. 

 
## Generalisation of the proof
We can generalise this by writing our vectors as $$\ket{a}$$, $$\ket{b}$$, $$\ket{c}$$. 

We then denote the vectors of our combined systems as $$\ket{a} \otimes \ket{c}$$ and  $$\ket{b} \otimes \ket{c}$$

Performing our copying transform again we get:

$$C(\ket{a} \otimes \ket{c}) = \ket{a} \otimes \ket{a}$$

$$C(\ket{b} \otimes \ket{c}) = \ket{b} \otimes \ket{b}$$


Now taking the inner products: 

$$(\ket{a} \otimes \ket{c}, \ket{b} \otimes \ket{c}) = \braket{a|b}\braket{c|c}=\braket{a|b}$$

$$(\ket{a} \otimes \ket{a}, \ket{b} \otimes \ket{b}) = \braket{a|b}\braket{a|b}=\braket{a|b}^2$$