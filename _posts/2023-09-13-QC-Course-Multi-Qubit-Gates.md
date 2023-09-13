---
layout: post
title: Basic Quantum Computing - Multi Qubit Systems
author: Charles Thomas
---

Last time, we talked about single qubit gates, but to do anything really interesting we need to make use of multiple qubits.

## Describing Multi Qubit Systems
Before we talk about gates acting on multiple qubits, we need to talk about describing systems of multiple qubits.

When we had 1 qubit, there were only two possible outcomes when we measured a qubit: 0 and 1. So we used two ket vectors to describe a qubit:

$$\ket{0} \text{ and }\ket{1}$$

Now if I have two qubits, then when I measure the system, I could get four outcomes: 00, 01, 10 and 11. So I need to use 4 ket vectors to describe a two qubit system:

$$\ket{00},\ket{01},\ket{10} \text{ and }\ket{11}$$

## Notation
So in general I can write a two qubit system as:

$$a\ket{00} + b\ket{01} + c\ket{10} + d\ket{11}$$


We can now extend this to 3 qubits:

$$a\ket{000} + b\ket{001} + c\ket{010} + d\ket{011} + e\ket{100} + f\ket{101} + g\ket{110} + h\ket{111}$$


In fact, we can describe a system of n qubits in this way, we just keep adding kets.


Let's return the two qubit system and quickly talk about notation. We originally wrote the two qubit system as:

$$a\ket{00} + b\ket{01} + c\ket{10} + d\ket{11}$$

But you might also see it written as:

$$a\ket{0}_A\ket{0}_B + b\ket{0}_A\ket{1}_B + c\ket{1}_A\ket{0}_B + d\ket{1}_A\ket{1}_B$$

when we want to make it obvious which of the two qubits is which.

Or even as:

$$a(\ket{0}\otimes\ket{0}) + b(\ket{0}\otimes\ket{1}) + c(\ket{1}\otimes\ket{0}) + d(\ket{1}\otimes\ket{1})$$

These all mean the same thing but just are different ways of writing it down.


We can also use the column vector syntax to describe a two qubit system. Now since we have 4 kets we need to have 4 entries. So 

$$a\ket{00} + b\ket{01} + c\ket{10} + d\ket{11}$$

becomes

$$\begin{bmatrix}a \\ b \\ c \\d\end{bmatrix}$$


## Swap Gates
Now, we can talk about some simple gates for two qubit systems. One of the most simple gates is the SWAP gate. This gate swaps two qubits so it takes:

$$a\ket{0}_A\ket{0}_B + b\ket{0}_A\ket{1}_B + c\ket{1}_A\ket{0}_B + d\ket{1}_A\ket{1}_B$$

And sends it to:

$$a\ket{0}_B\ket{0}_A + b\ket{0}_B\ket{1}_A + c\ket{1}_B\ket{0}_A + d\ket{1}_B\ket{1}_A$$

which we can rewrite as:

$$a\ket{0}_A\ket{0}_B + c\ket{0}_A\ket{1}_B + b\ket{1}_A\ket{0}_B + d\ket{1}_A\ket{1}_B$$


We can represent this using the following matrix:

$$\begin{bmatrix}
1 & 0 & 0 & 0\\
0 & 0 & 1 & 0\\
0 & 1 & 0 & 0\\
0 & 0 & 0 & 1\\
\end{bmatrix}
$$

And we'll use the following symbol:

{:style="text-align:center;"}
![Swap Gate](/assets/multiqubits/swapgate.png){: width="250" }

## Controlled Gates
Now we have two qubits, it would be nice if we can do some logic, where a gate only has an effect if another qubit is in a particular state. We can do this with the concept of controlled gates. 

To get to grips, with this, we'll work through an example: the CNOT gate. The CNOT gate or controlled not gate takes in two qubits: a control qubit and a target qubit. If the control qubit is 1 then it applies a NOT gate to the target qubit.

So let's consider the simple system:

$$a\ket{0}_C\ket{0}_T$$

where C represents the control qubit and T represents the target qubit.

Since the control qubit is 0 the CNOT gate does not change this state. But if we consider

$$a\ket{1}_C\ket{0}_T$$

Since the control qubit is 1 it will change the target qubit to 1 so we get:


$$a\ket{1}_C\ket{1}_T$$

We can put this all together for a general two qubit system. So if I have:

$$a\ket{0}_C\ket{0}_T + b\ket{0}_C\ket{1}_T + c\ket{1}_C\ket{0}_T + d\ket{1}_C\ket{1}_T$$

Then a CNOT gate will flip the target qubit where the control qubit is 1. So we get:

$$a\ket{0}_C\ket{0}_T + b\ket{0}_C\ket{1}_T + c\ket{1}_C\ket{1}_T + d\ket{1}_C\ket{0}_T$$

$$=a\ket{0}_C\ket{0}_T + b\ket{0}_C\ket{1}_T + d\ket{1}_C\ket{0}_T + c\ket{1}_C\ket{1}_T$$

So we can represent the CNOT gate with the following matrix:

$$\begin{bmatrix}
1 & 0 & 0 & 0\\
0 & 1 & 0 & 0\\
0 & 0 & 0 & 1\\
0 & 0 & 1 & 0\\
\end{bmatrix}
$$

And we use the following symbol:

{:style="text-align:center;"}
![CNOT Gate](/assets/multiqubits/cnot.png){: width="250" }

We can take this idea of a controlled gate and apply to other gates that we've seen e.g. we could make a controlled Y gate that only applies a Y gate is the control qubit is 1.

## Single Qubit Gates on Multi Qubit Systems
Finally, let's talk about how we can use the single qubit gates we learnt about last time in our multi qubit system.

Let's take our Hadamard gate from last time which did the following:

