---
layout: post
title: Basic Quantum Computing - Quantum Annealing
author: Charles Thomas
---

So far what we've talked about is called gate based Quantum Computing because we use quantum logic gates to write our algorithms. But there is another approach to quantum computing called quantum annealing. In this post we'll explore what quantum annealing is and how it works.

## What is an optimisation problem?
Before we can understand quantum annealing we need to discuss optimisation problems. An optimisation problem is where we have a problem and there are multiple possible solutions but we want to find the best one subject.

For example, I might want to send someone some presents but I need to buy some boxes to send them in, what is the smallest number of boxes I need to fit them all in. (You can read more about this problem [here](https://en.wikipedia.org/wiki/Bin_packing_problem))

## An unexpected optimisation problem

Even problem that do not at first seem like optimisation problems, can be rewritten as ones.

Consider solving $$1 + x = 2$$, instead of solving this algebraically we can consider it as an optimisation problem. Imagine someone proposes y as being some solution to this equation, then $$(1 + y) - 2$$ describes how good a solution it is. 

If y is very close to the correct answer then $$(1 + y) - 2$$ will be very close to zero and if it is far away from the correct answer then $$(1 + y) - 2$$ will be far away from zero.

In fact, if we square it to get $$((1 + y) - 2)^2$$ then it is 0 for the correct solution and gets further away from 0 for solutions that are less correct.

This means that solving $1 + x = 2$ is the same as optimising $$((1 + x) - 2)^2$$ 

## What is quantum annealing?

Quantum annealing is a way of solving optimisation problems using quantum physics. This means it is not quite as general as the gate based quantum computers we have seen before but it is still a powerful tool.

At a high level, the way it works it is to take a physical system of qubits. We can then choose a configuration of these qubits. This setup of qubits then has some lowest energy state. We can then put the qubits physically into this lowest energy state and measure their energy.

If we can pick our configuration carefully, we can pick a configuration such that the lowest energy of that configuration corresponds with the answers to our optimisation problem.

This probably sounds rather strange and abstract so we'll work throught a more concrete example.


## Understanding the Hamiltonian
We start with some qubits. The first thing to know is that qubits are often represents by the spin of some particle. We won't dive into what spin is but for our purposes all we need to know is that spin can either be up and have value +1 or be down and have value -1

The energy of these qubits is given by a mathematical expression called the Hamiltonian.

The first part of the Hamiltonian is 

$$\sum_i h_i \sigma_i$$ 

where $$h_i$$ is a is a number and $$\sigma_i$$ represents whether the ith qubit is spin up (+1) or spin down (-1)

The number $$h_i$$ is often called the bias

So for two qubits the following is a valid Hamiltonian: 

$$0.5 * 1 + 0.4*(-1)$$

The second term part of the Hamiltonian is 

$$\sum_{i,j,j>i} J_{i,j}\sigma_i\sigma_j$$

where $$J_{i,j}$$ is a real number called the coupling and $$\sigma_i$$, $$\sigma_j$$ represents the spins of the ith and jth qubits

What is expression means is that for every pair of qubits (we only want to count each pair once which is why we sum over j > i) we can put in a number.

In total, the Hamiltonian is of the form:


$$H = \sum_i h_i \sigma_i + \sum_{i,j,j>i} J_{i,j}\sigma_i\sigma_j$$

## Using the Hamiltonian to solve problems


## Sampling problems