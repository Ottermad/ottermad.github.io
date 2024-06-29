---
layout: post
title: Basic Quantum Computing - Shor's Algorithm - Using Order Finding
author: Charles Thomas
---

In this series of posts, we're exploring a famous algorithm called Shor's Algorithm. In this post, we will split it unto two parts: a quantum part and a classical part and then we will explain the classical part 


# Order Finding

Shor's algorithm can be split into two parts.

The first part is the part you need a quantum computer for: order finding.

Order finding deals with the following problem: 

Given a two numbers x and N what is the smallest integer $$r > 1$$ such that $$x^r \mod N = 1$$. This smallest r is called the order. 

For now we'll assume we have the algorithm to do this and we'll show how we can use this to factor a number.


# Factoring with Order Finding
So let's start with number we want to factor, call it N. We can use order finding to create an algorithm to find a factor, f, of it. (Remember a factor that divides another e.g. 3 is a factor of 6)

We can then divide N by this factor to get N/f and f

If N/f or f is not prime we repeat this process on them until we get all the prime factors.

So how do we find this factor f?

## Step 1
Well if N is even we know a prime factor is 2, so we're done.

## Step 2
Next we check if we can write N as 

$$N = a^b$$ for $$a, b > 0 \in \mathbb{Z}$$ 

If we can then a is a factor and we can return it. 

We can do this efficiently with a classical algorithm (Check out this [link](https://www.ams.org/journals/mcom/1998-67-223/S0025-5718-98-00952-1) for the details) 

## Step 3

Now we randomly pick a number y between 1 and N - 1

We compute the $$gcd(y, N)$$  (which we can do quickly thanks to Euclid's algorithm which we'll talk about in another post)

If $$gcd(y, N) > 1$$ then y is a factor of N so we can return y


## Step 4
Otherwise if $$gcd(y, N) = 1$$ then y and N are co prime (there is no prime number that  divides both of them)

So we consider the function $$f(r) = y^r \mod N$$

We then apply order finding to find the smallest r, such that

$$y^r \mod N = 1$$ 

which is the same as

$$y^r - 1 \mod N = 0$$

If r is odd, then we go back to step 3 and use a different y

If r is even, then we can factorise to get

$$(y^{r/2} - 1)(y^{r/2} + 1) \mod N = 0$$

This tells us that there is some integer k such that

$$(y^{r/2} - 1)(y^{r/2} + 1) = kN$$

## Step 5
Now we check that $$y^{r/2} - 1$$ and $$y^{r/2} + 1$$ are not multiples of N. 

We do this by computing 

$$gcd(y^{r/2} - 1, N)$$ and $$gcd(y^{r/2} + 1, N)$$. 

If either of these are equal to N then at least one of them is a multiple of N so we try again with a different y.

If they're both not equal to N then at least one of them must share a factor with N. So at least one of 

$$gcd(y^{r/2} - 1, N)$$, $$gcd(y^{r/2} + 1, N)$$ 

is a factor of N. 

So we can then repeat this on N/f and f until we get all the factors of N.

# Computing GCDs

You'll have noticed that for this to work we need to be able to compute the GCD of two numbers quickly. Thankfully, we can do that with a process called the Euclidean algorithm which we will explore in the next post.

# Worked Example

Let's try to factor 210

## The First Factor
We first check if it is even (this is step 1). 210 is even so we get 2 is a factor and we're left with 105

## The Second Factor
Now, we try to factor 105

105 is odd (step 1) and it can't be written as $$a^b$$ (step 2)

So we pick a number randomly between 1 and 104 (step 3)

Let's pick 57

Now we compute gcd(57, 105) = 3

This tells us 3 is a factor

## The Third Factor
We know that 105/3 = 35 so we now need to factor 35

35 is odd (step 1) and can't be written as $$a^b$$ (step 2)

Now we apply step 3 and we pick a random number between 1 and 34

So let's pick 6

We compute gcd(6, 35) = 1

So we have to go to step 4

So we are considering $$f(r) = 6^r \mod 35$$

And we apply order finding to get

$$r = 2$$

2 is even so we can write

$$(6 + 1)(6 - 1) = 7*5 = k * 35$$

So now we compute

$$gcd(7, 35) = 7$$ 

$$gcd(5, 35) = 5$$

Neither of these are equal to N we get the remaining factors of N as 7 and 5

## The End Result
So in total we get $$210 = 2 * 3 * 7 * 5$$