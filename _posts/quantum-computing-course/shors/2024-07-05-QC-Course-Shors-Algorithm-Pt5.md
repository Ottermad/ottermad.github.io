---
layout: post
title: Basic Quantum Computing - Shor's Algorithm - Euclid's Algorithm
author: Charles Thomas
---

In this series of posts, we're exploring a famous algorithm called Shor's Algorithm. In the last post, we saw how to use order finding to factorise a number. This relied on being able to quickly compute the gcd of two numbers. Thankfully we can do this fast classically using Euclid's algorithm.

# Euclid's Algorithm
Euclid's algorithm starts with two numbers a and b. We want to compute the $$gcd(a,b)$$

So we start by assuming $$a > b$$ then we can divide a by b to get a integer $$q_0$$ and a remainder $$r_0$$

Then we can write a as $$a = q_0 b + r_0$$

Then we consider $$b$$ and $$r_0$$. We know that $$r_0 < b$$. As if it was bigger then we can write 

$$a = q_0b + b + c = (q_0 + 1)b + c$$ 

which means we didn't do our division properly.

Now we write 

$$b = q_1 r_0 + r_1$$ 

and repeat this. So we write 

$$r_0 = q_2 r_1 + r_2$$

We do this until we get 

$$r_i = 0$$, 

then 

$$r_{i-1}$$ 

is the gcd of a and b.

We can see this by substituting everything back in. This gives us

$$r_{i-2} = q_i r_{i-1}$$

Which means

$$q_{i-3} = q_{i-1}r_{i-2} + r_{i-1} = q_{i-1} q_i r_{i-1}  + r_{i-1} = (q_{i-1} q_i  + 1) r_{i-1}$$

And so on until we get a in terms of $$r_{i-1}$$ and b.

# Example
Let's take a look at an example. Starting with 21 and 104 we want to compute $$gcd(21, 105)$$

We start by doing $$105 \div 21 = 4$$ remainder $$20$$ so we write $$104 = 4 * 21 + 20$$

Then we write $$21 = 1 * 20 + 1$$

And $$20 = 20 * 1 + 0$$

So the last non zero remainder is 1 so $$gcd(21, 105) = 1$$