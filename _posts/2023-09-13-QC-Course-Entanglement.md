---
layout: post
title: Basic Quantum Computing - Entanglement
author: Charles Thomas
---

You might have heard of heard of quantum entanglement and how spooky it is. But in this post we'll dive into what it really is.

## Two qubit systems
Entanglment is a phenomenon that happens between two or more quanutm systems. For us, we'll use qubits.

So let's recap from last time that we can describe a two qubit system as:

$$a\ket{0}_A\ket{0}_B + c\ket{0}_A\ket{1}_B + b\ket{1}_A\ket{0}_B + d\ket{1}_A\ket{1}_B$$

## Product states
Now let's look at an example of a two qubit states. Let's consider:

$$\frac{1}{\sqrt{2}}\ket{0}_A\ket{0}_B + \frac{1}{\sqrt{2}}\ket{0}_A\ket{1}_B$$

In this example 

$$a = b = \frac{1}{\sqrt{2}}$$

$$c = d = 0$$

Notice how we have

$$\ket{0}_A$$ 

in both terms so we can factor it out to:

$$\frac{1}{\sqrt{2}}(\ket{0}_A)(\ket{0}_B + \ket{1}_B)$$

This means we can write this state as a product of a term containing only A kets and another term containing only B kets.

When we can do this we say the state is a product state. 

## Entangled states
An entangled state is any state that is not a product state. So consider 

$$\frac{1}{\sqrt{2}}\ket{0}_A\ket{0}_B + \frac{1}{\sqrt{2}}\ket{1}_A\ket{1}_B$$

Here we can't write it as a product state because there is no term that occurs in both parts of the sum. So this is an entangled state.

## Measuring two qubit states
So we've learnt entangled states are just states that aren't product states, but why do we care? To answer this we need to talk about measuring two qubit systems.

We know if we have a two qubit state:

$$a\ket{0}_A\ket{0}_B + c\ket{0}_A\ket{1}_B + b\ket{1}_A\ket{0}_B + d\ket{1}_A\ket{1}_B$$

then the probability of measuring both qubits to be 0 is given by 

$$P(\ket{00}) = a\overline{a}$$

But what is the probability of getting just the first qubit to be 0. Well it's the probability of getting both qubits to be 0 or getting the first qubit to 0 and the second qubit to be 1. So we get:

$$P(\ket{0}_A) = P(\ket{00}) + P(\ket{01}) = a\overline{a} + c\overline{c}$$

So far we've talked about measuring both qubits simultaneously but what happens if I just measure one qubit. To figure this out let's work through an example:

So we start with:

$$a\ket{0}_A\ket{0}_B + c\ket{0}_A\ket{1}_B + b\ket{1}_A\ket{0}_B + d\ket{1}_A\ket{1}_B$$

Now we measure the first qubit and find it is 0.This means we can rid of the two terms because we know there is no way for the first qubit to be 1. So we're left with:

$$a\ket{0}_A\ket{0}_B + c\ket{0}_A\ket{1}_B$$

However, we can't guarantee:

$$a\overline{a} + c\overline{c} = 1$$ 

So something else must have happened. Well in order to guarantee that the probabilites sum to 1 we can divide by the square root of the probability that we got 0 in the first qubit. So we get:


$$\frac{1}{\sqrt{P(\ket{0}_a)}}(a\ket{0}_A\ket{0}_B + c\ket{0}_A\ket{1}_B)$$

$$=\frac{1}{\sqrt{a\overline{a} + c\overline{c}}}(a\ket{0}_A\ket{0}_B + c\ket{0}_A\ket{1}_B)$$

This guarantees the probabilities sum to 1 because our two new coeffients are:

$$\frac{a}{\sqrt{a\overline{a} + c\overline{c}}}$$

and 

$$\frac{c}{\sqrt{a\overline{a} + c\overline{c}}}$$


Since the denominators real when we work out the sum of the probabilities we get:

$$\frac{a}{\sqrt{a\overline{a} + c\overline{c}}}\frac{\overline{a}}{\sqrt{a\overline{a} + c\overline{c}}}
 + \frac{c}{\sqrt{a\overline{a} + c\overline{c}}}\frac{\overline{c}}{\sqrt{a\overline{a} + c\overline{c}}}$$

$$=\frac{a\overline{a} + c\overline{c}}{a\overline{a} + c\overline{c}} = 1$$

In summary, when we measure the first qubit and find it is a 0 we are left with the state:

$$\frac{1}{\sqrt{a\overline{a} + c\overline{c}}}(a\ket{0}_A\ket{0}_B + c\ket{0}_A\ket{1}_B)$$

Similarly, if we instead measure the second qubit and find it is a one we are left with:

$$\frac{1}{\sqrt{P(\ket{1}_b)}}(b\ket{0}_A\ket{1}_B + d\ket{1}_A\ket{1}_B)$$

$$=\frac{1}{\sqrt{b\overline{b} + d\overline{d}}}(b\ket{0}_A\ket{1}_B + d\ket{1}_A\ket{1}_B)$$


## Measuring entangled states
Finally, we're able to talk about why entangled states are so weird. Consider the following state of two qubits:

$$\frac{\ket{00}}{\sqrt{2}} + \frac{\ket{11}}{\sqrt{2}}$$


Now, let's keep the first qubit and send the second qubit miles away.

Let's measure the first qubit. If we find it is 0 we are left with:

$$\ket{00}$$

So the second qubit must be 0.

But if we find the first qubit is 1 we are left with:

$$\ket{11}$$

So somehow, when we measured one qubit in an entangled pair it seems we are able to affect the second qubit instantaneously which is very strange but as it turns out very useful.
