---
layout: post
title: Basic Quantum Computing - No Cloning Theorem
author: Charles Thomas
---

Note: This is a rework of an earlier post. You can checkout the original [here](https://ottermad.github.io/2021/12/22/No-Cloning-Theorem.html)

## What is the No Cloning Theorem?
In normal computers, we can copy the state of a bit. This is used all of the time. For instance, we might take the output of one operation and feed it into several others. When we do this at the circuit level this is called fanout.

But, we cannot do this with Quantum Computers. This is because it is impossible to copy an arbitrary quantum state - a result known as the No Cloning Theorem.

## Why does it matter?

The No Cloning Theorem causes problems when it comes to designing quantum circuits as we cannot use fanout. 

It also means we cannot use a common technique for error correction called checkpointing. Checkpointing is where you make a backup of the current state of a value part-way through a process.  So that in the case it gets corrupted you do not have to start the calculation from scratch. Instead, you can resume it from your last checkpoint.

We generally cannot do this in a quantum computer because we cannot copy arbitrary quantum states. This is problematic because quantum computers are very sensitive to errors. Hence, quantum error correction is a very active area of research.

# Proof of the No Cloning Theorem
We are going to do a proof by contradiction.

Let's assume that we have a unitary matrix C that can clone arbitrary quantum states.

Initially, we have arbitrary two quantum states 

$$\ket{A}\otimes\ket{B}$$ 

We want to clone the first vector so end up with:

$$\ket{A}\otimes\ket{A}$$ 


To do this we use the matrix C. So

$$C(\ket{A}\otimes\ket{B}) = \ket{A}\otimes\ket{A}$$


Let's do the cloning a second time:

$$C(\ket{E}\otimes\ket{B}) = \ket{E}\otimes\ket{E}$$

Now, we need to know two more facts. Firstly unitary matrices conserve inner products and secondly, we need to know how to calculate the inner products between multi qubit states.

The inner product between multi-qubit states are given by the following formula:

$$(\ket{a}\otimes\ket{b}) \cdot (\ket{c}\otimes\ket{d}) = \braket{a|c}\braket{c|d} $$ 

Now let's finish off the proof:

Let's take the inner product between our states before cloning:

$$(\ket{A}\otimes\ket{B})\cdot(\ket{E}\otimes\ket{B}) = \braket{A|E}\braket{B|B} = \braket{A|E}$$

Doing the same thing after cloning we have:

$$(\ket{A}\otimes\ket{A})\cdot(\ket{E}\otimes\ket{E}) = \braket{A|E}\braket{A|E} = \braket{A|E}^2$$

But since C conserved inner products we have:

$$\braket{A|E}=\braket{A|E}^2$$

which only has two solutions:

$$\braket{A|E} = 0$$ 

or 

$$\braket{A|E} = 1$$ 

This is a problem because it either means that A and E cannot be arbitrary. This is a contradiction.
