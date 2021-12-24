---
layout: post
title: Deutsch Jozsa Algorithm
author: Charles Thomas
---

The Deutsch Jozsa Algorithm is a quantum algorithm that solves a problem with few practical applications. It is notable for being one of the earliest demonstrations of a problem that can be solved faster on a quantum computer than on a classical computer.

# The Problem
Imagine we have a black box (called an oracle) that computes a function that accepts an n-bit binary string and returns either 0 or 1.

We know that the function is either:
* constant (e.g. always returns 1 or always returns 0) 
* balanced (returns 0 for half the inputs and 1 for the other half)

We want to work out which one the function is using the black box as little as possible.

# Classical Solution
If our function accepts an n bit string then there are $$2^n$$ inputs. To work out whether the function is balanced or constant we need to check one more than half the inputs. This means we have to check $$\frac{2^n}{2}+1=2^{n-1}+1$$ times.

# Quantum Solution
We can solve it on a quantum computer only using our black box once. To do we need to implement our oracle as transformation that maps the state $$\ket{x}\ket{y}$$ to $$\ket{x}\ket{y \oplus f(x)}$$ where $$\oplus$$ is addition modulo 2.


## The Setup
Let's take a 3 qubit system 

$$\ket{0}\otimes\ket{0}\otimes\ket{1}$$


## The First Hadamard
We then apply a Hadamard transform to every qubit:

$$(H\otimes H\otimes H)(\ket{0}\otimes\ket{0}\otimes\ket{1})$$

$$=H\ket{0} \otimes H\ket{0} \otimes H\ket{1}$$

$$=\frac{\ket{0}+\ket{1}}{\sqrt{2}} \otimes \frac{\ket{0}+\ket{1}}{\sqrt{2}} \otimes \frac{\ket{0}-\ket{1}}{\sqrt{2}}$$

$$=\frac{1}{2}(\ket{00} + \ket{01} + \ket{10} + \ket{11})\otimes \frac{\ket{0}-\ket{1}}{\sqrt{2}}$$

$$=\frac{1}{2\sqrt{2}}(\ket{00}(\ket{0}-\ket{1}) + \ket{01}(\ket{0}-\ket{1}) + \ket{10}(\ket{0}-\ket{1}) + \ket{11}(\ket{0}-\ket{1}))$$

$$=\frac{1}{2\sqrt{2}}(\ket{00}\ket{0}-\ket{00}\ket{1} + \ket{01}\ket{0}-\ket{01}\ket{1} + \ket{10}\ket{0}-\ket{10}\ket{1} + \ket{11}\ket{0}-\ket{11}\ket{1})$$

## Using the Oracle
Next we apply our oracle, O, so we map $$\ket{x}\ket{y}$$ to $$\ket{x}\ket{y \oplus f(x)}$$

$$O(\frac{1}{2\sqrt{2}}(\ket{00}\ket{0}-\ket{00}\ket{1} + \ket{01}\ket{0}-\ket{01}\ket{1} + \ket{10}\ket{0}-\ket{10}\ket{1} + \ket{11}\ket{0}-\ket{11}\ket{1}))$$

$$=\frac{1}{2\sqrt{2}}(\ket{00}\ket{0\oplus f(00)}-\ket{00}\ket{1\oplus f(00)} + \ket{01}\ket{0\oplus f(01)}-\ket{01}\ket{1\oplus f(01)} + \ket{10}\ket{0\oplus f(10)}-\ket{10}\ket{1\oplus f(10)} + \ket{11}\ket{0\oplus f(11)}-\ket{11}\ket{1\oplus f(11)})$$

Since $$0 \otimes x = x$$ because it is adding 0 we get:
 
$$=\frac{1}{2\sqrt{2}}(\ket{00}\ket{f(00)}-\ket{00}\ket{1\oplus f(00)} + \ket{01}\ket{f(01)}-\ket{01}\ket{1\oplus f(01)} + \ket{10}\ket{f(10)}-\ket{10}\ket{1\oplus f(10)} + \ket{11}\ket{f(11)}-\ket{11}\ket{1\oplus f(11)})$$

Now we can factor it to get:

$$=\frac{1}{2\sqrt{2}}(\ket{00}(\ket{f(00)}-\ket{1\oplus f(00)}) + \ket{01}(\ket{f(01)}-\ket{1\oplus f(01)}) + \ket{10}(\ket{f(10)}-\ket{1\oplus f(10)}) + \ket{11}(\ket{f(11)}-\ket{1\oplus f(11)})$$

Next we can write it as a sum:

$$=\frac{1}{2\sqrt{2}}\sum_{x=00}^{x=11}\ket{x}(\ket{f(x)}-\ket{1\oplus f(x)})$$

Since $$f(x)$$ is 0 or 1, if $$f(x)=0$$ then 

$$\ket{f(x)}-\ket{1\oplus f(x)}=\ket{0}-\ket{1\oplus 0}=\ket{0}-\ket{1}$$

If $$f(x)=1$$

$$\ket{f(x)}-\ket{1\oplus f(x)}=\ket{1}-\ket{1\oplus 1}=\ket{1}-\ket{0}$$

So we can write these as a single expression:

$$(-1)^{f(x)}(\ket{0}-\ket{1})$$

Substituting this into our sum we get:

$$\frac{1}{2\sqrt{2}}\sum_{x=00}^{x=11}(-1)^{f(x)}\ket{x}(\ket{0}-\ket{1})$$

## The Second Hadamard
We now disregard the final qubit so we're left with the state:

$$\frac{1}{2}\sum_{x=00}^{x=11}(-1)^{f(x)}\ket{x}$$

The n dimensional Hadamard can be written has a matrix with the elements:

$$(H_{n})_{i,j}=\frac{1}{2^{n/2}}(-1)^{i \cdot j}$$

Where i is row number and j is column number and $$i \cdot j$$ is the bitwise dot product of the binary representations of i and j. (Note: we start counting i and j from 0)

For example, $$3 \cdot 2 = (1,1) \cdot (1,0) = 1*1 + 1*0 = 1$$

To make it easier we're going to write i and j directly in their binary representations.

We can think of our vectors $$\ket{00},\ket{01}..$$ as column vectors with all zeros apart from in one place. This means they pick out a column of the Hadamard matrix. 

For example $$H_2\ket{00}$$ is the first column the Hadamard matrix. So we can write this as:

$$H_2\ket{00}=\sum_{y=00}^{11}\frac{1}{2^{2/2}}(-1)^{00\cdot y}\ket{y}$$

Now using this we can write applying the Hadamard to our 2 qubits above as:

$$H_2(\frac{1}{2}\sum_{x=00}^{11}(-1)^{f(x)}\ket{x})$$

$$=\frac{1}{2}\sum_{x=00}^{11}(-1)^{f(x)}(\sum_{y=00}^{11}\frac{1}{2}(-1)^{x\cdot y}\ket{y})$$ 

Pulling the $$\frac{1}{2}$$ out the front we get

$$=\frac{1}{2}\frac{1}{2}\sum_{x=0}^{11}(-1)^{f(x)}(\sum_{y=0}^{11}(-1)^{x\cdot y}\ket{y})$$ 

Next, we can pull the $$(-1)^{f(x)}$$ inside the second sum.

$$=\frac{1}{4}\sum_{x=0}^{11}(\sum_{y=0}^{11}(-1)^{f(x)}(-1)^{x\cdot y}\ket{y})$$ 

And finally we can swap the order of sums:

$$=\frac{1}{4}\sum_{y=00}^{11}\sum_{x=00}^{11}(-1)^{f(x)}(-1)^{x\cdot y}\ket{y}$$ 

## Making a measurement
In Quantum Mechanics, when we make a measurement, the probability of getting a result is the magnitude squared of the coefficient of that state.

If we measure our 2 qubits the probability of getting 00 is the magnitude squared of our $$y=\ket{00}$$ component. This is:

$$(\frac{1}{4}\sum_{x=00}^{11}(-1)^{f(x)}(-1)^{x\cdot 00})^2$$

Since $${x\cdot 00}$$ will always be 0 this simplfies to:

$$(\frac{1}{4}\sum_{x=00}^{11}(-1)^{f(x)})^2$$

Now if $$f(x)$$ is constant then our sum will be $$+4$$ or $$-4$$ which substituting back in gives us 1

If f(x) is balanced then our sum will contain 2 -1s and 2 +1s so the total will be 0.

So we'll definitely measure our two qubits to be in the state $$\ket{00}$$ if the function is constant and we'll never measure it to be in $$\ket{00}$$ if the function is balanced.

# Building an Oracle
Now, this algorithm relies on us being able to actually construct on our Oracle, so let's discuss how can go out of it.

## Oracle for Constant functions
Our final qubit is in the state: 

$$\frac{\ket{0}-\ket{1}}{2}$$

If $$f(x)=0$$ we want it to end up in the state:

$$\frac{\ket{f(x)}-\ket{1 \otimes f(x)}}{\sqrt{2}}=\frac{\ket{0}-\ket{1 \otimes 0}}{\sqrt{2}}=\frac{\ket{0}-\ket{1}}{\sqrt{2}}$$

So we can just apply I to our final qubit so we don't change it at all

If $$f(x)=1$$ then we want our state to be:

$$\frac{\ket{f(x)}-\ket{1 \otimes f(x)}}{\sqrt{2}}=\frac{\ket{01}-\ket{1 \otimes 1}}{\sqrt{2}}=\frac{\ket{1}-\ket{0}}{\sqrt{2}}$$


So we can apply a quantum NOT gate (also called an X gate) to it. This is will swap 0 and 1 around.

## Oracle for balanced functions
There are several ways to build a balanced oracle. We'll explore a single one.

Before we apply our oracle we have the state:

$$\frac{1}{2\sqrt{2}}(\ket{00}(\ket{0}-\ket{1}) + \ket{01}(\ket{0}-\ket{1}) + \ket{10}(\ket{0}-\ket{1}) + \ket{11}(\ket{0}-\ket{1}))$$

We have four two qubit states: $$\ket{00}$$, $$\ket{01}$$, $$\ket{10}$$, $$\ket{11}$$. 

2 of them have an even number of ones, 2 of them have an odd number of ones. 

This means we can build a balanced state using CNOT gates.

CNOT gates take in two qubits: if the first bit (known as the control bit) is 0 then it does nothing to the second bit. If the first bit is 1 it flips the second bit.

If we set up a CNOT gate for our first n qubits. For each CNOT the control bit will be one of the n qubits and our final qubit will be the output bit.

Now looking back at our state, if we have an even number of 1s in our input then nothing will change. If we have an odd number of ones we'll end up changing the sign.

This means 

$$\frac{1}{2\sqrt{2}}(\ket{00}(\ket{0}-\ket{1}) + \ket{01}(\ket{0}-\ket{1}) + \ket{10}(\ket{0}-\ket{1}) + \ket{11}(\ket{0}-\ket{1}))$$

will become

$$\frac{1}{2\sqrt{2}}(\ket{00}(\ket{0}-\ket{1}) - \ket{01}(\ket{0}-\ket{1}) - \ket{10}(\ket{0}-\ket{1}) + \ket{11}(\ket{0}-\ket{1}))$$


# Generalising
Assume we n+1 qubits with the first n in the state $$\ket{0}$$ and the final one in the state $$\ket{1}$$ Our combined state is:

$$\ket{0}^{\otimes n}\ket{1}$$

If we consider our first n qubits set to 0, their state space is spanned by $$2^n$$ basis vectors

Applying a Hadamard gate to each of the first n, we make every possible state equally likely so we get:

$$(\frac{1}{\sqrt{2^n}}\sum_{x=0}^{2^{n-1}}\ket{x}) \otimes \ket{1}$$

Now applying a Hadamard to the final qubit in the state $$\ket{1}$$ we get

$$(\frac{1}{\sqrt{2^n}}\sum_{x=0}^{2^{n-1}}\ket{x}) \otimes \frac{\ket{0}-\ket{1}}{\sqrt{2}}$$

$$=\frac{1}{\sqrt{2^{n+1}}}\sum_{x=0}^{2^{n-1}}\ket{x}(\ket{0}-\ket{1})$$

This time when we applying the oracle we get:

$$\frac{1}{\sqrt{2^{n+1}}}\sum_{x=0}^{2^{n-1}}\ket{x}(\ket{f(x)}-\ket{1\oplus f(x)})$$

$$=\frac{1}{\sqrt{2^{n+1}}}\sum_{x=0}^{2^{n-1}}(-1)^{f(x)}\ket{x}(\ket{0}-\ket{1})$$

Now let's discard the last qubit to get:

$$\frac{1}{\sqrt{2^{n}}}\sum_{x=0}^{2^{n-1}}(-1)^{f(x)}\ket{x}$$

Now applying the Hadamard using our formula from earlier

$$H_n(\frac{1}{\sqrt{2^{n}}}\sum_{x=0}^{2^{n-1}}(-1)^{f(x)}\ket{x})$$

$$=\frac{1}{\sqrt{2^{n}}}\sum_{x=0}^{2^{n-1}}(-1)^{f(x)} (\sum_{y=0}^{2^{n-1}}\frac{1}{2^{n/2}}(-1)^{x\cdot y}\ket{y})$$

$$=\frac{1}{2^n}\sum_{y=0}^{2^{n-1}}\sum_{x=0}^{2^{n-1}}(-1)^{f(x)}(-1)^{x\cdot y}\ket{y}$$

Now find the probability that we get all 0s:

$$\frac{1}{2^n}\sum_{x=0}^{2^{n-1}}(-1)^{f(0)}(-1)^{x\cdot 0}$$

$$=\frac{1}{2^n}\sum_{x=0}^{2^{n-1}}(-1)^{f(0)}$$

which once again is 1 is the function is constant and 0 is the balanced

