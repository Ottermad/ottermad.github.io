---
layout: post
title: Basic Quantum Computing - Super dense coding
author: Charles Thomas
---

Note:This is a rework of an earlier post. You can checkout the original [here](https://ottermad.github.io/2021/12/23/Super-Dense-Coding.html)

We are finally ready to look at some applications of quantum computation. We're going to start by looking at super dense coding which allows us to send 2 classical bits of information by sending one qubit.


# The Setup
Alice and Bob want to be able to communicate. So a third party (Charlie) takes two qubits and puts them in the state

$$\frac{\ket{0}_A\ket{0}_B + \ket{1}_A\ket{1}_B}{\sqrt{2}}$$

Afterwards, he sends qubit A to Alice and qubit B to Bob.

# Sending information
Alice wants to send 2 classical bits of information to Bob. That means she wants to send Bob: 00, 10, 01 or 11. 

Depending on which of these 4 she wants to send she'll perform a different transformation on her qubit before sending it to Bob.(Since Bob does nothing this is represented by the identity transform I)

## Sending 00
Now if Alice wants to send 00 she does nothing so the system stays in the state:

$$\frac{\ket{0}_A\ket{0}_B + \ket{1}_A\ket{1}_B}{\sqrt{2}}$$

## Sending 01
If Alice wants to send 01 then she applies the NOT gate (aka the X gate).

This just swaps the 0 and 1 in her qubit so she gets:

$$\frac{\ket{1}_A\ket{0}_B + \ket{0}_A\ket{1}_B}{\sqrt{2}}$$


## Sending 10
If Alice wants to send 10 then she applies the Z gate.

$$Z = \begin{bmatrix}1 & 0 \\ 0 & -1 \end{bmatrix}$$

We can work out the matrix for this using the formula from a couple of lessons ago:

$$(Z \otimes I) = \begin{bmatrix}1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & -1 & 0 \\ 0 & 0 & 0 & -1 \\\end{bmatrix}$$

$$(Z \otimes I)(\frac{\ket{0}_A\ket{0}_B + \ket{1}_A\ket{1}_B}{\sqrt{2}})$$ 

$$= \begin{bmatrix}1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & -1 & 0 \\ 0 & 0 & 0 & -1 \\\end{bmatrix}
\frac{1}{\sqrt{2}}
\begin{bmatrix}1 \\ 0 \\ 0 \\ 1 \\\end{bmatrix}
= 
\frac{1}{\sqrt{2}}
\begin{bmatrix}1 \\ 0 \\ 0 \\ -1 \\\end{bmatrix}
= 
\frac{\ket{00} - \ket{11}}{\sqrt{2}}
$$


## Sending 11
If Alice wants to send 11 then she applies the iY gate (this is a new gate but it's very similar to the Y gate we've seen before).

$$iY = i\begin{bmatrix}0 & -i \\ i & 0 \end{bmatrix}=\begin{bmatrix}0 & 1 \\ -1 & 0 \end{bmatrix}$$

$$(iY \otimes I) = \begin{bmatrix}0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \\ -1 & 0 & 0 & 0 \\ 0 & -1 & 0 & 0 \\\end{bmatrix}$$

$$(iY\otimes I)(\frac{\ket{0}_A\ket{0}_B + \ket{1}_A\ket{1}_B}{\sqrt{2}})$$

$$=\begin{bmatrix}0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \\ -1 & 0 & 0 & 0 \\ 0 & -1 & 0 & 0 \\\end{bmatrix}
\frac{1}{\sqrt{2}}
\begin{bmatrix}1 \\ 0 \\ 0 \\ 1 \\\end{bmatrix}
= 
\frac{1}{\sqrt{2}}
\begin{bmatrix}0 \\ 1 \\ -1 \\ 0 \\\end{bmatrix}
= 
\frac{\ket{01}-\ket{10}}{\sqrt{2}}
$$


# Bob receives information
Alice now sends her qubit to Bob. Now Bob has both qubits, he applies two gates on the qubits, a controlled not (CNOT) followed by a Hadamard gate.

$$(H \otimes I)(CNOT)$$

$$=\frac{1}{\sqrt{2}}\begin{bmatrix}1 & 0 & 1 & 0 \\ 0 & 1 & 0 & 1 \\ 1 & 0 & -1 & 0 \\ 0 & 1 & 0 & -1 \\\end{bmatrix}\begin{bmatrix}1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 0 & 1 \\ 0 & 0 & 1 & 0 \\\end{bmatrix}$$

$$=\frac{1}{\sqrt{2}}\begin{bmatrix}1 & 0 & 0 & 1 \\ 0 & 1 & 1 & 0 \\ 1 & 0 & 0 & -1 \\ 0 & 1 & -1 & 0 \\\end{bmatrix}$$

Bob now measures both qubits so he gets one of: 00, 01, 10 or 11. So he's gotten two bits of classical information but Alice only had to send him one qubit.


## Worked example
Let's work through an example.

So we start by making the system:

$$\frac{\ket{0}_A\ket{0}_B + \ket{1}_A\ket{1}_B}{\sqrt{2}}$$

Now we send one to Alice and one to Bob.

Alice now wants to send 01 to Bob. So she applies the NOT gate to her qubit to get:

$$\frac{\ket{1}_A\ket{0}_B + \ket{0}_A\ket{1}_B}{\sqrt{2}}$$

She now sends the qubit to Bob.

Bob now applies the CNOT gate followed by the Hadamard gate to both qubits:

$$=\frac{1}{\sqrt{2}}\begin{bmatrix}1 & 0 & 0 & 1 \\ 0 & 1 & 1 & 0 \\ 1 & 0 & 0 & -1 \\ 0 & 1 & -1 & 0 \\\end{bmatrix}\frac{1}{\sqrt{2}}\begin{bmatrix}0 \\1\\1\\0\end{bmatrix}$$

$$=\frac{1}{2}\begin{bmatrix}0 \\1+1\\0 \\1-1\end{bmatrix} = \begin{bmatrix}0 \\1\\0 \\0\end{bmatrix}$$

$$=\ket{01}$$

So when he measures both qubits he will always get 01 which is what Alice wanted to send.
