---
layout: post
title: Super dense coding
author: Charles Thomas
---

Take two qubits $$\ket{a}$$ and $$\ket{b}$$. Let's create an combined system of them:

$$\ket{a} \otimes \ket{b} = \frac{\ket{00} + \ket{11}}{\sqrt{2}} = \begin{bmatrix}1 \\ 0 \\ 0 \\ 1 \\\end{bmatrix}$$

Send one qubit to Alice. Send the other to Bob.

Now if Alice wants to send 00 she does nothing so the system stays in the state:

$$\frac{\ket{00} + \ket{11}}{\sqrt{2}}$$

If Alice wants to send 01 then she applies the transform Z.

$$(Z \otimes Z)(\ket{a} \otimes \ket{b}) = 
\begin{bmatrix}1 & 0 & 0 & 0 \\ 0 & -1 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & -1 \\\end{bmatrix}
\frac{1}{\sqrt{2}}
\begin{bmatrix}1 \\ 0 \\ 0 \\ 1 \\\end{bmatrix}
= 
\frac{1}{\sqrt{2}}
\begin{bmatrix}1 \\ 0 \\ 0 \\ -1 \\\end{bmatrix}
= 
\frac{\ket{00} - \ket{11}}{\sqrt{2}}
$$


If Alice wants to send 10 then she applies the transform X.

$$(X \otimes X)(\ket{a} \otimes \ket{b}) = 
\begin{bmatrix}0 & 1 & 0 & 0 \\ 1 & 0 & 0 & 0 \\ 0 & 0 & 0 & 1 \\ 0 & 0 & 1 & 0 \\\end{bmatrix}
\frac{1}{\sqrt{2}}
\begin{bmatrix}1 \\ 0 \\ 0 \\ 1 \\\end{bmatrix}
= 
\frac{1}{\sqrt{2}}
\begin{bmatrix}0 \\ 1 \\ 1 \\ 0 \\\end{bmatrix}
= 
\frac{\ket{10} + \ket{01}}{\sqrt{2}}
$$


If Alice wants to send 11 then she applies the transform iY.

$$(iY\otimes iY)(\ket{a} \otimes \ket{b}) = 
\begin{bmatrix}0 & 1 & 0 & 0 \\ -1 & 0 & 0 & 0 \\ 0 & 0 & 0 & 1 \\ 0 & 0 & -1 & 0 \\\end{bmatrix}
\frac{1}{\sqrt{2}}
\begin{bmatrix}1 \\ 0 \\ 0 \\ 1 \\\end{bmatrix}
= 
\frac{1}{\sqrt{2}}
\begin{bmatrix}0 \\ -1 \\ 1 \\ 0 \\\end{bmatrix}
= 
\frac{-\ket{10} + \ket{01}}{\sqrt{2}}
$$

The four possible states of the system form a orthogonal basis. This means if Bob goes to measure his qubit in this new basis he will know the state of the whole system.