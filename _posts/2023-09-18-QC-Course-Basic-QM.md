---
layout: post
title: Basic Quantum Mechanics For Quantum Computing
author: Charles Thomas
---

We finally know enough mathematics that we can start delving into quantum mechanics.

## Representing states
To get started with quantum mechanics, let's imagine we have a coin. When we flip a coin, we find that it can either be heads or tails. We say the coin is either in the heads state or the tails state. Let's represent this using

$$\ket{H} = \text{Coin is heads}$$

$$\ket{T} = \text{Coin is tails}$$

Now, so far this is the same as classical physics. We have a system that can be one of two states. But here's where stuff gets a little weird. In Quantum Mechanics, the states form a complex vector space. What this means is that if I have one state, then all multiples of that state are also possible. If it also means if I have two or more states then all linear combinations of those states are possible.

So in the case of our quantum coin, we don't have just have the two states above we have all the linear combinations of them. So all the states of the form

$$a\ket{H} + b\ket{T}$$

where a, b are complex numbers are possible.

## Measuring states
Already, quantum mechanics has got a little weird but it is about to get stranger. If I have a state of the form:

$$a\ket{H} + b\ket{T}$$

when I measure it I will find that the coin is either heads or tails. So the state becomes either

$$\ket{H}\text{ or }\ket{ T }$$

What this means is that even though the coin can be in this more general state, when I perform a measurement on it then it changes. This is strange because it means you can't measure a system without possibly changing it.

We say that when we do a measurement the state collapses.

Now, we can ask if we can know what the state will collapse into? Well, we can't know exactly but we can know the probability.

For a state:

$$a\ket{H} + b\ket{T}$$

Then the probability of measuring heads is given by:

$$P(\ket{H}) = a\overline{a}$$

And the probability of measuring tails is given by:

$$P(\ket{T}) = b\overline{b}$$

So this imposes an important restriction on what states are possible. Since we know probabilities add up to 1 we must have:

$$a\overline{a} + b\overline{b} = 1$$

for all valid quantum states.

For example:

$$\frac{1}{\sqrt{2}}\ket{H} + \frac{1}{\sqrt{2}}\ket{T}$$

is a valid quantum state because

$$\frac{1}{\sqrt{2}}\overline{\frac{1}{\sqrt{2}}} + \frac{1}{\sqrt{2}}\overline{\frac{1}{\sqrt{2}}} = \frac{1}{2} + \frac{1}{2} = 1$$


But 

$$3\ket{H} + 4\ket{T}$$

is not as 

$$3\overline{3} + 4\overline{4} = 25$$

## Phases
Back when we learning about complex numbers, we found that numbers of the form:

$$e^{it}$$

have modulus 1. Which means that

$$e^{it}\overline{e^{it}} = e^{it}e^{-it} = 1$$

This means for any quantum state, I can multiply any of the coefficients by a number of this form without changing the probabilities of what I'll measure.

This is because if I have

$$a\ket{H} + e^{it}b\ket{T}$$

then

$$e^{it}b\overline{e^{it}b} = e^{it}be^{-it}\overline{b} = b\overline{b}$$

We call this number:

$$e^{it}$$

a phase.

As we'll see in a future post, the phase difference between the coefficients actually can be detected. This means:

$$a\ket{H} + e^{it}b\ket{T}$$

is different to

$$a\ket{H} + b\ket{T}$$

However, if the phase applies to the whole state:

$$e^{it}(a\ket{H} + b\ket{T})$$ 

then we cannot determine this difference so it is the same as:

$$a\ket{H} + b\ket{T}$$

If a phase applies to the whole we call it a global phase.


## Evolving states
Finally, we can talk about how quantum states change in time. In general, a quantum state changes in time according to some unitary matrix U.

The reason the matrix must be unitary is that unitary matrices conserve probabilities. What I mean by this is that if we start with a vector v such that

$$a\overline{a} + b\overline{b} = 1$$

Then multiplying a vector by a unitary matrix does not change this fact.

Now, how do we know what unitary matrix to use? Well for a closed system - that is a system where nothing interferes with it it evolves according to the Hamiltonian - which you can think of as describing the energy of the system.

However, in Quantum Computing, we actually deal with open systems because we force the state to evolve in certain ways, so we can the unitary matrix that we want to use.

## Qubits
Now, so far we've talked about a quantum coin. But in quantum computer science, we talk about qubits. Now a qubit is just another quantum system but instead of using:

$$a\ket{H} + b\ket{T}$$

we use

$$a\ket{0} + b\ket{1}$$

## Braket notation
Finally, let's talk a bit about this notation we've been using. We started by writing:

$$\ket{H}$$ 

to represent our quantum coin being heads. This is fancy symbol around the H just means it is a vector and we call it a ket vector.

So 

$$\ket{T}$$

is also a ket vector.

Now, ket seems like a strange name but I promise it will make sense in a moment. If we turn a ket around we get a bra vector:

$$\bra{H}$$

We won't worry too much about the differences between bras and kets for now. The important thing is that we can combine bras and kets and write

$$\braket{H|H}$$

This combination of a bra and ket (a bracket) stands for taking the inner product between the two vectors.

## Orthogonality
This is important because we have one last special thing to note about our quantum states. 

$$\ket{0} \text{ and } \ket{1}$$  

They are orthonormal. What this means is that:

$$\braket{1|1} = 1$$

$$\braket{0|0} = 1$$

$$\braket{0|1} = 0$$
