---
layout: post
title: Measurement in Quantum Mechanics
author: Charles Thomas
---

When we talk about measuring some value we don't give it a lot of thought. But this changes when you are working with Quantum Mechanics.  The results of your measurements probabilistic and you will also change the system itself by the act of measuring it.

This makes working with Quantum Mechanical systems much harder than you might expect. In this post, we'll explore how measurements are represented mathematically in Quantum Mechanics.

You may find it helpful to check out my previous post on the mathematics for quantum mechanics.

# General Measurements
When we perform a measurement on a quantum system, we get one of a discrete set of values. For instance, if we measure the spin of a particle we'll get back up either up (+1) or down (-1).

We represent this mathematically with a set of operators (matrices). Where each operator corresponds to a possible result of the measurement. So if we have three possible outcomes of a measurement: a, b and c. Then we will have a set of three operators: 

$$\{M_a, M_b, M_c\}$$

Since we must account for all possible outcomes our set of operators must obey a completeness relation: 

$$\sum_n{M_n^{\dagger}M_n} = I$$

When we do a measurement M the probability of getting state a for a given state vector, w, is 

$$\bra{w}M_a^{\dagger}M_a\ket{w}$$

In Quantum Mechanics, doing a measurement changes the state of the system. If we measure the system, w, to be in the state a then our wave function will now be

$$\frac{M_a\ket{w}}{\sqrt{\bra{w}M_a^{\dagger}M_a\ket{w}}}$$

# Projective Measurements
There is a more common way of formulating measurements in QM called projective measurements.

Projective measurements are when we impose that all our measurement operators, Ms, are Hermitian, orthogonal and projectors.

Hermitian means $$M_a = M_a^{\dagger}$$

Orthogonal means $$\bra{M_a}\ket{M_b} = \delta_{a,b}M_a$$

Projector means $$(M_a)^n = M_a$$

Applying these properties we get the probability of getting result a is

$$p(a) = \bra{w}M_a^{\dagger}M_a\ket{w}= \bra{w}M_a^2\ket{w} = \bra{w}M_a\ket{w}$$

And the state after the measurement is:

$$\frac{M_a\ket{w}}{\sqrt{\bra{w}M^{\dagger}M\ket{w}}}=\frac{M_a\ket{w}}{\sqrt{p(m)}}$$

You can then define an operator called an observable, P, where
$$P = \sum_n{nM_n}$$ where n is the value of measurement $M_n$

It should also be noted that each n is an eigenvalue of the observable.

## Why use projective measurements?
One reason for doing this is that it makes calculating the average value of a measurement of a particular state. E.g. if I prepare many systems in a state $\ket{w}$ then do measure observable P what will the average/mean of my results be?

This is called the expectation value. It is is calculated by summing all values of possible results multiplied by the probability of getting them. 

$$E(P) = \sum_n{np(n)}$$

Applying our results above we get

$$E(P) = \sum_n{n\bra{w}M_n\ket{w}} = \sum_n{\bra{w}nM_n\ket{w}} = \bra{w}(\sum_n{nM_n})\ket{w} = \bra{w}P\ket{w}$$

$$\bra{w}P\ket{w}$$ is often denoted $$\braket{P}$$

## Projective Measurements and Unitary transformations give general measurements
From general measurements, we can get projective measurements. But is it possible to get general measurements from projective measurements?

It is possible to if we use the idea that quantum systems evolve in time according to unitary transformations.

Let's start with a quantum system $$Q$$ 

We want to implement general measurement 

$$M = \{M_a, M_b ....\}$$

To do this we introduce a second quantum system $$R$$ which has basis vectors $$r_n$$ which map one to one with our measurement operators

Let $$\ket{0}$$ be a fixed vector in R and $$\ket{\phi}$$ be any vector in Q. 

Now consider states $$\ket{0}\ket{\phi}$$ in the combined space $$Q \otimes R$$

We create unitary transform 

$$U\ket{0}\ket{\phi} = \sum_n{M_n\ket{r_n}\ket{\phi}}$$ 

(We will show that it unitary in the section below)

Now consider the projective measurement given by the projectors 

$$P_n = I_Q \otimes \ket{r_n}\bra{r_n}$$ 

applied to 

$$U\ket{0}\ket{\phi}$$

Using our forumla for probability of getting n when measuring state: $$U\ket{0}\ket{\phi}$$

$$p(n) = \bra{\phi}\bra{0}U^{\dagger}P_n U\ket{0}\ket{\phi}$$

Substitute in $$P_n$$

$$ \bra{\phi}\bra{0}U^{\dagger}(I_Q \otimes \ket{r_n}\bra{r_n})U\ket{0}\ket{\phi}$$

And now our formula for U

$$\sum_{n', n''}\bra{\phi}\bra{r_{n'}}M_{n'}^{\dagger}(I_Q \otimes \ket{r_n}\bra{r_n})M_{n''}\ket{r_{n''}}\ket{\phi}$$

By the orthogonality of $$r_n$$ when $$n = n' = n''$$ we will get $$\bra{r_a}\ket{r_b}=1$$ and other we will get 0. Combine this with the fact that $$I_q$$ does nothing.

$$\bra{\phi}M_n^{\dagger}M_n\ket{\phi}$$

which is exactly our result for general measurement.

To get the formula for the post measurement state of $$U\ket{0}\ket{\phi}$$ we will apply the projective measurement formula:

$$\frac{P_nU\ket{0}\ket{\phi}}{\sqrt{p(n)}}$$

Substituting in $$P_n$$ and U we get 

$$\frac{(I_Q \otimes \ket{r_n}\bra{r_n})\sum_{n'}{M_{n'}\ket{r_{n'}}\ket{\phi}}}{\sqrt{p(n)}}$$

Once again by orthogonality and $I_Q$ doing nothing we get:

$$\frac{M_n\ket{r_n}\ket{\phi}}{\sqrt{p(n)}}$$

Now put in our result for $p(n)$

$$\frac{M_n\ket{r_n}\ket{\phi}}{\sqrt{\bra{\phi}M_n^{\dagger}M_n\ket{\phi}}}$$

Therefore Q is in the state:

$$\frac{M_n\ket{\phi}}{\sqrt{\bra{\phi}M_n^{\dagger}M_n\ket{\phi}}}$$

which is again the formula for general measurement.

## Showing U is unitary
To show U is unitary we will do it in two steps. 

First, we'll show U is unitary on states of the form $$\ket{\phi}\ket{0}$$
Then we'll extend U to the whole space. 

To show U is unitary on states of the form $$\ket{\phi}\ket{0}$$ we need to show inner products are conserved.

$$\bra{0}\bra{\psi}U^{\dagger}U\ket{\phi}\ket{0}$$
$$=\sum_{nn'}{\bra{\psi}\bra{r_{n'}}M_{n'}^{\dagger}M_n\ket{r_n}\ket{\phi}}$$

Now we apply the orthonormality of $\ket{r_n}$ to get

$$=\sum_n\bra{\psi}M_{n}^{\dagger}M_n\ket{\phi}$$

Now by applying our completeness relation: $$\sum_n{M_n^{\dagger}M_n} = I$$

This reduces $$\bra{\psi}\ket{\phi}$$

Now we need to show that we can extend it to all states.

We will do this by proving the following general lemma:

If
* V is a Hilbert space
* W is a subspace of V
* U is a unitary operator on W


Then there exists a unitary operator, $$U'$$,  on V that agrees with U on W.

Since W is a subspace there exists the orthogonal complement of W,  a subspace $$W^{\perp}$$ which is all the other vectors in V that aren't in W plus the zero vector.

We can then write a basis for V. The first n basis vectors can in W, then the others will in $$W^{\perp}$$

So we can create the operator:

$$U'\ket{v} = U\sum_{n}\ket{v_n} + I\sum_{n+1}\ket{v_{n}}$$

which applies U to the basis vectors in W and the identity operator to those not.

The operator is unitary as both U and I are unitary and agrees on U as vectors in W will only been made up of basis vectors in W. 

Now applying this lemma we get our result.

# POVMs
There is another way of talking about measurements in Quantum Mechanics: POVMs. These are powerful when we only care about the result of measurement and not the state afterwards. This happens quite a lot in experiments where we do our measurement, get our result and move on.

This formulation is known as Positive Operator Valued Measure. Or POVM for short.

Here we take our set of measurement operators: $$\{M_a, M_b, M_c\}$$. And assigned to each of them a POVM element ($$E_n$$) using the formula 

$$E_n = M_n^{\dagger}M_n$$

The set of all the $$E_n$$s is called a POVM.

We can plug the $$E_n$$ in to our formula for probability to get: 

$$p(a) = \bra{w}M_a^{\dagger}M_a\ket{w} = \bra{w}E_a\ket{w}$$

In case we only have the POVM ($$\{E_n\}$$) we can't work out the state after the measurement because we don't know $$M_n^{\dagger}$$

## Why use POVMs?
We have seen two different ways of creating measurements from our general measurement principles. But why bother having both?

Well, this is because they are useful in different circumstances. POVMs are often more useful when dealing with the situation where it doesn't make sense to talk about post-measurement state of a system. For example, if we measure a photon with a silvered mirror that destroys the photon so there is not a post-measurement state.

POVMs can also be easier to work out from experiments because the $$E_i$$ do not need to projectors and can just read off the experiment results.
