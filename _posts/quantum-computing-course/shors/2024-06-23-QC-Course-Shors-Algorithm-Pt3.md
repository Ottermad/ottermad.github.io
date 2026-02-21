---
layout: post
title: Basic Quantum Computing - Shor's Algorithm - Introduction to RSA
author: Charles Thomas
---

In this series of posts, we're exploring a famous algorithm called Shor's Algorithm. In this post, well give a quick outline of how RSA works so you can understand why being able to efficiently factor large numbers is a problem for it.

# What is RSA?
RSA is a public key cryptosystem and this means there are two keys: a public key and a private key. The public key is used to encrypt the message and the private key is used to decrypt the message.

So if Bob wants to send Alice a message encrypted using the public key then he asks Alice to send him her public key (anyone can have access to the public key). Bob then uses the public key to encrypt the message. Bob then sends his encrypted message to Alice - it doesn't matter if anyone else reads it. They won't be able to decrypt it unless they have the private key which only Alice has. Alice receives the encrypted message and can read it using her private key.

# How does RSA work?
To generate the public and private keys RSA uses the following process:

1) Choose two distinct prime numbers: p, q

2) Compute $$n = pq$$

3) Compute the Carmichael's totient function of the product as $$\lambda(n) = lcm(p - 1, q - 1)$$

4) Choose any number $$2 < e < \lambda(n)$$ that is coprime (a and b are coprime if there is no prime number that  divides both of them) to $$\lambda(n)$$

5) Compute d, the modular multiplicative inverse of $$e \mod \lambda(n)$$ this means that $$de \mod \lambda(n) = 1$$

6) The public key is (n, e) and the private key is (n, d)

# Using RSA
So if Bob wants to send a message to Alice he takes his message m (represented as a number) and computes $$c = m^e \mod N$$

Then then sends the number c to Alice and then Alice computes $$c^d = (m^e)^d = m \mod N$$

Now the key idea here is that although e is known publicly, it is hard to work out d from e and n.

But if you can factor n then you can recover p and q, so you can compute $$\lambda(n)$$ and you can work out $$d = e^{-1} \mod \lambda(pq)$$