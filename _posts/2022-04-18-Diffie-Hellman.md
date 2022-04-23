---
layout: post
title: Diffie Hellman
author: Charles Thomas
---

As I've been studying Quantum Computing I came across Diffie Hellman but it took me a while to get my head around it. So I thought I would try to explain it.

# Symmetric Ciphers
To understand Diffie Hellman let's first talk about the concept of the symmetric cipher. A symmetric cipher is when we encrypt a message with one key and then use the same key to decrypt it.

As an example let's look at the Caesar cipher. The cipher starts by giving each letter a number. For example a becomes 1, b becomes 2 and so on. This means we can take a message made up of numbers and write it in letters. For example, hello becomes 8 5 12 12 15

Then to encrypt the message we add n to all the numbers. If n is 3 then our message would become 11 8 15 15 18. The important caveat is that if our number is bigger than 26 we go back to counting at 1. So if we have the letter y it has the number 25, then if we had 3 to it we would normally get 28 but in our case we get 2. (This is called modular arithmetic and we'll talk about more about it later).

So we now have our encrypted numbers 11 8 15 15 18. Let's turn it back into letters to get khoor. We can then send khoor to anyone we want. But if they want to decrypt it they need to know n i.e. how many places which shifted the letters.

So we need a way of safely sending n to a person so we can communicate using our ceaser cipher. Diffie Hellman allows us to solve this problem.


# Modular arithmetic
We'll need a bit of maths to understand Diffie Hellman. Firstly, we need to discuss modular arithmetic.

$$Z_p$$ is the set of integers (whole numbers) from 0 up to 1-p. We might write it as $$\{0, 1, 2,...., 1-p\}$$

Modular arithmetic is the same as normal arithmetic apart from if our number is bigger than $$1-p$$ we go wrap around back to to 0.

For example, if we're doing arithmetic modulo 7 (e.g. p = 7) we have 6 + 1 = 0. This might also be written $$(6 + 1) \mod 7 = 0$$. Where the $$\mod 7$$ tells us we're working modulo 7. 

When working with normal arithmetic we have the concept of equality e.g. $$5 + 1 = 4 + 2$$ When using modulo arithmetic we have the concept of congruence (represented by the symbol $$\equiv$$). 

Two numbers are congruent if we applied $$\mod n$$ to both sides and get the same number. For example, if we're working with $$\mod 12$$ then $$38 \equiv 14 (\mod 12)$$ because $$38\mod 12= 3$$ and $$14\mod 12 = 3$$

If we're performing a complicated calculation that is done $$\mod p$$ instead of doing to $$\mod p$$ at the end of calculation we can do it after each step of the calculation.  This is very useful when performing calculations on a computer, since it allows us to represent values in a fixed number of bits.

# Group Theory
The next bit of maths we'll need is some group theory. 

A group consists of two parts. The first part is the set (for our purposes a set is a collection of unique things) of elements $$E$$.

The second part is a binary operation $$\cdot$$. A binary operation is one that takes in two arguments. Our binary operation works by taking in two members of $$E$$ and giving us a back another member of $$E$$.

For $$E$$ and $$\cdot$$ to make up a group they need to have a few properties.

Firstly $$\cdot$$ must be associative. This means $$(a \cdot b) \cdot c$$ is the same as $$a \cdot (b \cdot c)$$ e.g. it doesn't matter where we put the brackets. 

The next property is the existence of the identity. This means there must be a special element of $$E$$ that we'll call $$e$$. Whenever we do $$e \cdot a$$ we get back $$a$$ no matter what a is. (This is like multiplying a number by 1 - you always get back itself).

The final property we need the existence of an inverse. This means for every element, a, in E there is another element b such that $$a \cdot b = e$$. E.g. there is always a way of undoing something. For example, if I multiply an number by 15 then multiplying by $$\frac{1}{15}$$ is its inverse.

## Abelian Groups
Some special groups have a fourth property called commutativity. This means that $$a \cdot b$$ is the same as $$b \cdot a$$. For example addition is commutative e.g. $$5 + 3 = 3 + 5$$ where as division is not $$\frac{5}{3} \neq \frac{3}{5}$$
If a group is commutative it is called Abelian. 

# Diffie Hellman
So how does this help us solve the problem of sharing the key for our cipher?

Let's start with Alice and Bob who want to share a key. Let's assume they can communicate over some insecure channel. This channel anyone can look at but no one can modify something during transmission.

They start by picking a group (we'll discuss which group later). They then pick an element g. 

Let's assume Alice wants wants to send a message to Bob. Bob starts picking a random integer k and calculate $$g^k$$. E.g. $$g \cdot g ...$$ k times. 

Bob keeps k secret but shares $$g^k$$ publicly (this is his public key).

Alice takes $$g^k$$ and then picks her own random number j

She computes $$g^j$ and $$(g^k)^j \mod p$$


She keeps j and $$(g^k)^j$$ secret. But she encrypts a message using $$(g^k)^j \mod p$$ as they key.

She sends the message and $$g^j$$ to Bob.

Bob now k, $$g^j$$ and the encrypted message.

Bob then calculates $$(g^j)^k \mod p$$ but this is the same as $$(g^k)^j$$ so he can decrypt the message.


# Security assumptions

Since the channel Alice and Bob are communicating on you'll notice p, g, g^k, g^j and the encryted message may be seen by an attacker. So how do we know that an attacker can't use this information to work $$(g^k)^j$$ and decrypted the message.

Well our first assumption is that given $$g^k$$ or $$g^j$$ it is hard to work out k or j respectively. This problem of working out k from $$g^k$$ is known as discrete logarithm problem. And we believe it is hard for certain groups (the ones Alice and Bob picked). This is known as the discrete logarithm assumption

We next must assume from g, g^k, g^j there is no way to easily work out $$(g^k)^j$$. This is called the computational diffie hellman assumption.

Finally, given g, g^j and g^k it must be hard to guess g^j^k Formally (g, g^j, g^k, g^j^k) must have nearly the same probability has (g, g^j, g^k, g^z) where z is random. This is known as the decisional diffie hellman assumption.



* g, g^k is public

* Channel is insecure
* Therefore g^j and the encrypted message may also be known by someone other than Alice or Bob
* It must be hard to work out k given g and g^k otherwise (g^j)^k could easily computed and the message decryped (hardness of discrete logs)
* It also most be hard computing (g^j)^k must be hard given only g, g^k and g^j (CDH)
* Also given g, g^j and g^k it must be hard to guess g^j^k Formally (g, g^j, g^k, g^j^k) must have nearly the same probability has (g, g^j, g^k, g^z) where z is random (DDH)

* Zp are integers {0, 1, 2,...., 1-p}
* We let it operations wrap around
* Modulo 7: 6 + 1 = 0
* Congruent if a = b mod p
* If calculation performed mod p we can reduce at each step
* Reduction modulo p is very useful when performing calculations on a computer, since it allows us to represent values in a fixed number of bits
* Curve25519 uses arithmetic modulo the prime number p = 2^255 − 19


* Set of elements E
* Associative 
* Identity
* Inverse
* Abelian Group - commutative 



* Allows two parties (Alice and Bob) to establish a shared secret by communicating over an insecure channel, under the assumption that the adversary can only observe but not modify the communication.
* g^k is the group operator applied to g k times
* Alice wants to send message to Bob
* Bob has public key g^k where k is picked randomly by Bob and g is public
* Alice gets Bob's public key g^k
* Alice picks random integer j
* Alice computes g^j and (g^k)^j
* Alice sends g^j to Bob
* Alice encrypts message to using (g^k)^j as the key and sends it to Bob
* Bob now has k, g^j and the encrypted message
* Bob computes (g^j)^k
* (g^j)^k = (g^k)^j
* Therefore Bob can decrypt the message