---
layout: post
title: No Cloning Theorem
author: Charles Thomas
---

In normal computers, we can copy the state of a bit. This is used all for the time. For instance, we might take the output of one operation and feed it into several others. When we do this at the circuit level this is called fanout.

But, we cannot do this with Quantum Computers. This is because it is impossible to copy an arbitrary quantum state - a result known as Quantum Computing.

This causes problems when it comes to designing quantum circuits as we cannot use fanout. It also means we cannot use a common technique for error correction called checkpointing. Checkpointing is where you make a backup of the current state of a value part way through a process.  So that in the case it gets corrupted you do not have to start the calculation from scratch. Instead you can resume it from your last checkpoint.

We generally cannot do this is in a quantum computer because we cannot copy arbitrary quantum states. This is problematic because quantum computers are very sensitive to errors. Hence, quantum error correction is a very active area of research.

Clearly, the no-cloning theorem causes some problems and I found it shocking when I first came across it.  So I thought I would outline a proof of this theorem in an accessible way. 


# Quantum Mechanics Intro

To do this we need to start with a little bit of quantum mechanics. You might find it useful to check out my post on the maths need for this [here](https://ottermad.github.io/2021/12/20/Basics-Maths-For-QM.html)

## Representing States
A qubit is represented by a vector $$\begin{bmatrix}a \\ b\end{bmatrix}$$ where $$a^2 + b^2 = 1$$ and a & b are complex numbers.

Multiple qubit systems are represented by the ‘kronecker product’ ($$\otimes$$) of the vectors so a system of two qubits:  $$\begin{bmatrix}a \\b \end{bmatrix}$$ and $$\begin{bmatrix}c \\ d\end{bmatrix}$$ represented as  $$\begin{bmatrix}a \\b \end{bmatrix} \otimes \begin{bmatrix}c \\ d\end{bmatrix}$$ which gives us the vector:  $$\begin{bmatrix}ac \\ ad \\ bc \\ bd\end{bmatrix}$$

## Measurements
There are two kinds of operations in quantum mechanics. The first is a measurement. These take a quantum state and put it in a definite state. This means it takes from being any vector and puts it into one of a certain number of states. 

For example a measurement might take a qubit and put it into either   $$\begin{bmatrix}1 \\ 0\end{bmatrix}$$ or  $$\begin{bmatrix}0 \\ 1\end{bmatrix}$$.

Since measurements reduce any vector to be one of a fixed number of vectors we cannot use measurements to clone any arbitrary state. This is because you most states e.g. $$\begin{bmatrix}0.3 \\ 0.7\end{bmatrix}$$ we'll end up changing it.

## Evolution
Quantum systems evolve  (change with time) according to unitary transformations. 

For our purposes, we can think of having a vector, v, that represents the current state of our systems. It can then change being multiplied by some matrix U to give a new vector, w,  which is the state of the system later on in time.

The matrix U has to unitary what that means that its inverse is the same as its conjugate transpose. These matrices have the special property that they preserve inner products.

# Proof of no-cloning
We are going to do a proof by contradiction.

Let's assume that we have a unitary matrix C that can clone arbitrary quantum states.

Initially have two vectors $$\begin{bmatrix}a \\b\end{bmatrix}$$ and $$\begin{bmatrix}c \\d\end{bmatrix}$$. We want to clone $$\begin{bmatrix}a \\b\end{bmatrix}$$ so we have two copies of it by overwriting $$\begin{bmatrix}c \\d\end{bmatrix}$$.

At first we have combined state vector $$\begin{bmatrix}ac \\ ad \\ bc \\ bd\end{bmatrix}$$

C acts on  $$\begin{bmatrix}ac \\ ad \\ bc \\ bd\end{bmatrix}$$ to give$$\begin{bmatrix}aa \\ ab \\ ab \\ bb\end{bmatrix}$$ 

Notice that c has gone to a and d has gone to b.

Now imagine we do the process again with   $$\begin{bmatrix}e \\f\end{bmatrix}$$ and $$\begin{bmatrix}c \\d\end{bmatrix}$$ so
$$C \begin{bmatrix}ec \\ ed \\ fc \\ fd\end{bmatrix}$$ becomes $$\begin{bmatrix}ee \\ ef \\ ef \\ ff\end{bmatrix}$$

Now take the inner product before we did the cloning

$$(\begin{bmatrix}ac \\ ad \\ bc \\ bd\end{bmatrix}, \begin{bmatrix}ec \\ ed \\ fc \\ fd\end{bmatrix})$$

$$= (ac)^* (ec) + (ad)^* (ed) + (bc)^* (fc) + (bd)^* (fd) $$

$$= a^* e(cc^* + dd^*) + d^*f (cc^* + dd^*) $$

$$= a^* e + d^*f$$


This time we take the inner products after the cloning we get:

$$(\begin{bmatrix}aa \\ ab \\ ab \\ bb\end{bmatrix}, \begin{bmatrix}ee \\ ef \\ ef \\ ff\end{bmatrix})$$

$$= a^* a^* ee + a^* b^* ef + a^* b^* ef + b^* b^* ff $$

$$= (a^* e)^2 + 2(a^* b^* ef) + (b^* f)^2$$

$$= (a^* e + b^* f)^2$$

Since C preserves inner products, these two answers must be the same. So 

$$a^* e + d^*f = (a^* e + b^* f)^2 $$. 

But the only solutions to this are:

$$(a^* e + b^* f) = 0$$ or $$(a^* e + b^* f) = 1$$ 

But this means  $$\begin{bmatrix}a \\b\end{bmatrix}$$ and  $$\begin{bmatrix}e \\f\end{bmatrix}$$ cannot be any two vectors which is a contradiction (specifically it tells us the states are either the same or orthogonal)

So there cannot exist a way of cloning arbitrary quantum states. 

 
## Generalisation of the proof
We can generalise this by writing our vectors as $$\ket{a}$$, $$\ket{b}$$, $$\ket{c}$$ where we are using the [bra-ket notation](https://en.wikipedia.org/wiki/Bra%E2%80%93ket_notation) to denote 3 arbitrary complex vectors.

We then denote the vectors of our combined systems as $$\ket{a} \otimes \ket{c}$$ and  $$\ket{b} \otimes \ket{c}$$

Using this notation we write the inner product between two vectors, 1 and 2, as 

$$\braket{1|2}$$

There is also an easy way to work out the inner products of combined systems. If we have two vectors $$\ket{1} \otimes \ket{2}$$ and  $$\ket{3} \otimes \ket{4}$$ the inner product between them is the inner product between $$\ket{1}$$ and $$\ket{3}$$ times the inner product of $$\ket{2}$$ and $$\ket{4}$$ which using our new notation is:

$$\braket{1|3}\braket{2|4}$$

Performing our copying transform again we get:

$$C(\ket{a} \otimes \ket{c}) = \ket{a} \otimes \ket{a}$$

$$C(\ket{b} \otimes \ket{c}) = \ket{b} \otimes \ket{b}$$


Now taking the inner products: 

$$(\ket{a} \otimes \ket{c}, \ket{b} \otimes \ket{c}) = \braket{a|b}\braket{c|c}=\braket{a|b}$$

$$(\ket{a} \otimes \ket{a}, \ket{b} \otimes \ket{b}) = \braket{a|b}\braket{a|b}=\braket{a|b}^2$$

Which once again means: 

$$\braket{a|b} = 0$$

or 

$$\braket{a|b} = 1$$