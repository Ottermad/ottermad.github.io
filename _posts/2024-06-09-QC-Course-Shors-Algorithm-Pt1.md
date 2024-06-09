---
layout: post
title: Basic Quantum Computing - Shor's Algorithm Introduction
author: Charles Thomas
---
In this series of posts, we're going to explore a famous algorithm called Shor's Algorithm. We'll break it down piece by piece so anyone can follow along. In this first post, I'll explain what problem it solves and why we should care about it.


# What problem does Shor's Algorithm solve?
Shor's Algorithm aims to solve the following problem: given some integer z decompose into its prime factors.

This might not make any sense so let's break it down. An integer is just a whole number like 1, 7 or 26.

Now we say an number a divides another number b if $$b \div a$$ is a whole number. 

So $$21 \div 7 = 3$$ so we say 7 divides 21. We often write this as $$7 \vert 21$$

A prime number is just an integer greater than 1 where the only two numbers that divide it are 1 and itself.

For example 7 is a prime number because out of 1, 2, 3, 4, 5, 6, 7 only 1 and 7 divide it.

It turns out that given some integer we can always write it has a product of prime numbers. For example $$12 = 4 \times 3 = 2 \times 2 \times 3$$

We call the prime numbers we use to write out a number its prime factors e.g. the prime factors of 12 are 2 and 3.

So Shor's Algorithm is an algorithm that takes in a number and gives us its prime factors e.g. the prime numbers we can multiply together to get our original number

# Why care about prime factors?
There are two related reasons we should care about having a quantum algorithm for factoring. Firstly, finding the prime factors of a number is believed (although not proved) to be classically hard. What we mean by this is that there is no efficient algorithm for finding the prime factors of a number using a classical computer.

This makes Shor's Algorithm important because it gives us a strong suggestion that quantum computers are more powerful than quantum computers.

The second reason to care about Shor's algorithm is that is will break a lot of cryptography systems. Cryptography systems are systems that allow us to encode our data in such a way that other people can't read it. 

These systems encode the data in such a way that you can't understand the data without the key which is what allows you to decode the data.

One very popular cryptography is called RSA and it relies on the assumption that prime factoring is hard. If you can factor prime numbers efficiently then any data encrpyted using RSA could be decrypted by anyone. So Shor's algorithm was also a big shock to the world for this reason.
