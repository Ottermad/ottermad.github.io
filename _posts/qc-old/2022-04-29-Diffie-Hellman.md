---
layout: post
title: Diffie Hellman
author: Charles Thomas
---

As I've been studying Quantum Computing I came across Diffie Hellman but it took me a while to get my head around it. So I thought I would try to explain it.

# Symmetric Ciphers
To understand Diffie Hellman let's talk about symmetric ciphers. A symmetric cipher is when we encrypt a message with one key and then use the same key to decrypt it.

As an example let's look at the Caesar cipher. The cipher starts by giving each letter a number. For example, a becomes 1, b becomes 2 and so on. This means we can take a message made up of letters and write it in numbers. For example, hello becomes 8 5 12 12 15

To encrypt the message we add n to all the numbers. If n is 3 then our message would become 11 8 15 15 18. The important caveat is that if our number is bigger than 26 we go back to counting at 1. Ff we have the letter y it has the number 25. Then if we add 3 to it we would normally get 28 but in our case, we get 2 (this is called modular arithmetic).

So we now have our encrypted numbers 11 8 15 15 18. Let's turn them back into letters to get khoor. We can then send khoor to anyone we want. But if they want to know what it means they need to know n i.e. how many places we have shifted the letters.

So we need a way of safely sending n to a person so we can communicate using our Ceaser cipher. Diffie Hellman allows us to solve this problem.


# Group Theory
The bit of maths we'll need is some group theory. 

A group consists of two parts. The first part is the set (for our purposes a set is a collection of unique things) of elements $$E$$.

The second part is a binary operation $$\cdot$$. A binary operation takes in two arguments. Our binary operation works by taking in two members of $$E$$ and giving us a back another member of $$E$$.

For $$E$$ and $$\cdot$$ to make up a group they need to have a few properties.

Firstly $$\cdot$$ must be associative. This means $$(a \cdot b) \cdot c$$ is the same as $$a \cdot (b \cdot c)$$ e.g. it doesn't matter where we put the brackets. 

The next property is the existence of the identity. This means there must be a special element of $$E$$ that we'll call $$e$$. Whenever we do $$e \cdot a$$ we get back $$a$$ no matter what a is. (This is like multiplying a number by 1 - you always get back itself).

The final property we need is the existence of an inverse. This means for every element, a, in E there is another element b such that $$a \cdot b = e$$. E.g. there is always a way of undoing something. For example, if I multiply a number by 15 then multiplying by $$\frac{1}{15}$$ is its inverse.

# Diffie Hellman
So how does this help us solve the problem of sharing the key for our cipher?

Let's start with Alice and Bob who want to share a key. Let's assume they can communicate over some insecure channel. This channel anyone can look at but no one can modify something during transmission.

They start by picking a group. They then pick an element g. 

Let's assume Alice wants to send a message to Bob. Bob starts picking a random integer k and calculates

$$g^k = g \cdot g ...$$ k times. 

Bob keeps k secret but shares $$g^k$$ publicly (this is his public key).

Alice takes $$g^k$$ and then picks her own random number j

She computes $$g^j$$ and $$(g^k)^j$$


She keeps j and $$(g^k)^j$$ secret. But she encrypts a message using $$(g^k)^j$$ as the key.

She sends the message and $$g^j$$ to Bob.

Bob now has k, $$g^j$$ and the encrypted message.

Bob then calculates $$(g^j)^k$$ but this is the same as $$(g^k)^j$$ so he can decrypt the message.


# Security assumptions

Since the channel Alice and Bob are communicating over isn't secure p, g, $$g^k$$, $$g^j$$ and the encrypted message may be seen by an attacker. So how do we know that an attacker can't use this information to work $$(g^k)^j$$ and decrypted the message.

Well our first assumption is that given $$g^k$$ or $$g^j$$ it is hard to work out k or j respectively. This problem of working out k from $$g^k$$ is known as the discrete logarithm problem. And we believe it is hard for certain groups. This is called the discrete logarithm assumption

We next must assume from g, $$g^k$$, $$g^j$$ there is no way to easily work out $$(g^k)^j$$. This is called the computational Diffie hellman assumption.

Finally, given g, $$g^j$$ and $$g^k$$ it must be hard to guess $$(g^j)^k$$ Formally $$(g, g^j, g^k, (g^j)^k)$$ must have nearly the same probability has $$(g, g^j, g^k, g^z)$$ where z is random. This is known as the decisional Diffie hellman assumption.

Not every group has all these properties so we have to pick the group carefully. Choosing the right group can be difficult so we'll explore that in another blog post.


# Summary
In summary, Diffie Hellman allows two people to create a shared key that they can use for a symmetric cipher while communicating over a public channel
