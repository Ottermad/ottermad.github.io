---
layout: post
title: Basic Quantum Computing - Teleportation
author: Charles Thomas
---

In super dense coding, we used a qubit to send 2 bits of classical information, quantum teleportation is a way of using classical bits to send a qubit.

## The Setup
Once again, we have Alice and Bob, they meet up and create a pair of qubits in the entangled state:

$$\frac{\ket{0}_A\ket{0}_B + \ket{1}_A\ket{1}_B}{\sqrt{2}}$$

They then go their seperate ways with one qubit each.


## Alice sends a qubit to Bob
Once day, Alice wants to send a qubit to Bob. 

Alice starts with the qubit

$$(a\ket{0} + b\ket{1})$$

So the combined system of three qubits is given by

$$(a\ket{0} + b\ket{1}) \otimes \frac{\ket{0}_A\ket{0}_B + \ket{1}_A\ket{1}_B}{\sqrt{2}}$$

$$=\frac{a\ket{00}_A\ket{0}_B + a\ket{01}_A\ket{1}_B + b\ket{10}_A\ket{0}_B + b\ket{11}_A\ket{1}_B}{\sqrt{2}}$$

Alice applies a CNOT gate on her two qubits. This changes her second qubit to a 1 if her first qubit is a 0 

$$=\frac{a\ket{00}_A\ket{0}_B + a\ket{01}_A\ket{1}_B + b\ket{11}_A\ket{0}_B + b\ket{10}_A\ket{1}_B}{\sqrt{2}}$$

giving followed by a Hadamard gate on the first qubit

$$=\frac{a\ket{00}_A\ket{0}_B}{2} + \frac{a\ket{10}_A\ket{0}_B}{2} + \frac{a\ket{01}_A\ket{1}_B}{2} + \frac{a\ket{11}_A\ket{1}_B}{2}$$

$$ +\frac{b\ket{01}_A\ket{0}_B}{2} - \frac{b\ket{11}_A\ket{0}_B}{2} + \frac{b\ket{00}_A\ket{1}_B}{2} - \frac{b\ket{10}_A\ket{1}_B}{2}$$

This leaves the state:

$$\frac{1}{2}(\ket{00}_A(a\ket{0}_B + b\ket{1}_B) + \ket{01}_A(b\ket{0}_B + a\ket{1}_B)$$

$$ + \ket{10}_A(a\ket{0}_B - b\ket{1}_B)) + \ket{11}_A(b\ket{0} _B-a\ket{1}_B)$$

Alice then measures her two qubits. She'll get one of 4 results: 00, 01, 10 and 11.

## Bob receives the qubit
She then send her results to Bob clasically.

Based on what Alice sends to him, Bob performs a unitary operation on his qubit:

If Bob receives 00 from Alice then the system is in the state:

$$\ket{00}_A(a\ket{0}_B + b\ket{1}_B)$$

So Bob has to do nothing (or does the identity transformation)

If Bob receives 01 from Alice then the system is in the state:

$$\ket{01}_A(b\ket{0}_B + a\ket{1}_B)$$

So Bob has to swap the co effients around so he applies the X gate

$$X = \begin{bmatrix}
    0 & 1 \\ 1 & 0
\end{bmatrix}$$

Which leaves him with 

$$\ket{01}_A(a\ket{0}_B + b\ket{1}_B)$$

If Bob receives 10 from Alice then the system is in the state:

$$\ket{10}_A(a\ket{0}_B - b\ket{1}_B))$$

So Bob has to change -b to b so he applies the Z gate

$$Z = \begin{bmatrix}
    1 & 0 \\ 0 & -1
\end{bmatrix}$$

This gives the final state as

$$\ket{10}_A(a\ket{0}_B + b\ket{1}_B))$$

Finally, if Bob receives 11 from Alice then the system is in the state:

$$\ket{11}_A(b\ket{0} _B-a\ket{1}_B)$$

Then he applies the following gate

$$iY = \begin{bmatrix}
    0 & -1 \\ 1 & 0
\end{bmatrix}$$

Leaving

$$\ket{11}_A(a\ket{0} _B+b\ket{1}_B)$$

This means no matter what Alice sends to him, at the end the state of Bob's system is

$$a\ket{0} _B+b\ket{1}_B$$ 

which is the qubit Alice wanted to send him.

If you're interest in my content like this please checkout the rest of my course that you can find [here]({% post_url 2023-09-25-QC-Course-Intro %}) or sign up to my [newsletter](https://open.substack.com/pub/charliethomas/p/weekly-newsletter-21th-december?r=6k919&utm_campaign=post&utm_medium=web)


