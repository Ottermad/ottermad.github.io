---
layout: post
title: Super dense coding
author: Charles Thomas
---

One interesting application of Quantum Computing the ability to transfer information using fewer bits. This is known as super dense coding.

Specifically, super dense coding allows us to send a 2 classical bits of information by sending one qubit.

To see how this works let's go through an example.

# The Setup
Alice and Bob want to be able to communicate. So a third party (Charlie) takes two qubits $$\ket{a}$$ and $$\ket{b}$$. And then creates an combined system of them:

$$\ket{a} \otimes \ket{b}$$

He then prepares the system in a special state:

$$\ket{a} \otimes \ket{b} = \frac{\ket{00} + \ket{11}}{\sqrt{2}} = \frac{1}{\sqrt{2}}\begin{bmatrix}1 \\ 0 \\ 0 \\ 1 \\\end{bmatrix}$$

Afterwards, he send one qubit to Alice and the other to Bob.

# Sending information
Alice wants to send 2 classical bits of information. That means she wants to send Bob: 00, 10, 01 or 11. Depending on which of these 4 she wants to send she'll perform a different transform on her qubit before sending it to Bob.

## Sending 00
Now if Alice wants to send 00 she does nothing so the system stays in the state:

$$\frac{\ket{00} + \ket{11}}{\sqrt{2}}=\frac{1}{\sqrt{2}}\begin{bmatrix}1 \\ 0 \\ 0 \\ 1 \\\end{bmatrix}$$

## Sending 01
If Alice wants to send 01 then she applies the transform X (this is also known as the Quantum NOT gate).

$$X = \begin{bmatrix}0 & 1 \\ 1 & 0 \end{bmatrix}$$

$$(X \otimes I) = \begin{bmatrix}0 & I \\ I & 0 \end{bmatrix}$$

$$(X \otimes I)(\ket{a} \otimes \ket{b}) = 
\begin{bmatrix}0 & 1 & 0 & 0 \\ 1 & 0 & 0 & 0 \\ 0 & 0 & 0 & 1 \\ 0 & 0 & 1 & 0 \\\end{bmatrix}
\frac{1}{\sqrt{2}}
\begin{bmatrix}1 \\ 0 \\ 0 \\ 1 \\\end{bmatrix}
= 
\frac{1}{\sqrt{2}}
\begin{bmatrix}0 \\ 1 \\ 1 \\ 0 \\\end{bmatrix}
= 
\frac{\ket{10} + \ket{01}}{\sqrt{2}}
$$

## Sending 10
If Alice wants to send 10 then she applies the transform Z.

$$Z = \begin{bmatrix}1 & 0 \\ 0 & -1 \end{bmatrix}$$

$$(Z \otimes I) = \begin{bmatrix}I & 0 \\ 0 & -I \end{bmatrix}$$

$$(Z \otimes I)(\ket{a} \otimes \ket{b}) = 
\begin{bmatrix}1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & -1 & 0 \\ 0 & 0 & 0 & -1 \\\end{bmatrix}
\frac{1}{\sqrt{2}}
\begin{bmatrix}1 \\ 0 \\ 0 \\ 1 \\\end{bmatrix}
= 
\frac{1}{\sqrt{2}}
\begin{bmatrix}1 \\ 0 \\ 0 \\ -1 \\\end{bmatrix}
= 
\frac{\ket{00} - \ket{11}}{\sqrt{2}}
$$


## Sending 11
If Alice wants to send 11 then she applies the transform iY.

$$iY = i\begin{bmatrix}0 & -i \\ i & 0 \end{bmatrix}=\begin{bmatrix}0 & 1 \\ -1 & 0 \end{bmatrix}$$

$$(iY \otimes I) = \begin{bmatrix}0 & I \\ -I & 0 \end{bmatrix}$$

$$(iY\otimes I)(\ket{a} \otimes \ket{b}) = 
\begin{bmatrix}0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \\ -1 & 0 & 0 & 0 \\ 0 & -1 & 0 & 0 \\\end{bmatrix}
\frac{1}{\sqrt{2}}
\begin{bmatrix}1 \\ 0 \\ 0 \\ 1 \\\end{bmatrix}
= 
\frac{1}{\sqrt{2}}
\begin{bmatrix}0 \\ 1 \\ -1 \\ 0 \\\end{bmatrix}
= 
\frac{\ket{01}-\ket{10}}{\sqrt{2}}
$$

# Getting the information back
The four possible states of the system form a orthogonal basis. This means it is possible to distinguish between these four states. Therefore, Bob can measure which of the four states he has with certainty and work out what he was sent.


# Bonus: Changing Basis
Bob can do the measurement above because the four states form an orthogonal basis. In fact, they form a special basis called the Bell Basis. But it is possible to put these back in the basis we're used to (which is called the computational basis).

To do this once Bob has both qubits, does two transform on the qubits, a controlled not (CNOT) followed by a Hadamard gate.

## CNOT
The controlled not (CNOT) gate is a Quantum gate that works on two qubits. It's name comes from the fact that if the first qubit (known as the control bit) is 0 it does nothing to second qubit. But if the first qubit is 1 then it negates the second qubit.

It is represented by the matrix:
$$\begin{bmatrix}1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 0 & 1 \\ 0 & 0 & 1 & 0 \\\end{bmatrix}$$

## Hadamard gate

$$H = \frac{1}{\sqrt{2}}\begin{bmatrix}1 & 1 \\ 1 & -1 \end{bmatrix}$$

$$H \otimes I = \frac{1}{\sqrt{2}}\begin{bmatrix}I & I \\ I & -I \end{bmatrix}=\begin{bmatrix}1 & 0 & 1 & 0 \\ 0 & 1 & 0 & 1 \\ 1 & 0 & -1 & 0 \\ 0 & 1 & 0 & -1 \\\end{bmatrix}$$

## Together 

$$(H \otimes I)(CNOT)$$

$$=\frac{1}{\sqrt{2}}\begin{bmatrix}1 & 0 & 1 & 0 \\ 0 & 1 & 0 & 1 \\ 1 & 0 & -1 & 0 \\ 0 & 1 & 0 & -1 \\\end{bmatrix}\begin{bmatrix}1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 0 & 1 \\ 0 & 0 & 1 & 0 \\\end{bmatrix}$$

$$=\frac{1}{\sqrt{2}}\begin{bmatrix}1 & 0 & 0 & 1 \\ 0 & 1 & 1 & 0 \\ 1 & 0 & 0 & -1 \\ 0 & 1 & -1 & 0 \\\end{bmatrix}$$

This matrix will convert a vector in the Bell basis to the computational basis.
