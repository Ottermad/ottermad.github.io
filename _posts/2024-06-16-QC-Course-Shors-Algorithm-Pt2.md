---
layout: post
title: Basic Quantum Computing - Shor's Algorithm - Introduction to number theory
author: Charles Thomas
---

In this series of posts, we're exploring a famous algorithm called Shor's Algorithm. In this post, we're going to dive into the basic number theory we're going to need to understand it.

# Greatest Common Divisors
First, let's recap the definition of a prime number: an integer greater than 1 where the only two numbers that divide it are 1 and itself.

We've also said that we say an integer a divides another integer b if $$b \div a$$ is a whole number.

Now if we have two integer a and b and a third integer c divides both a and b e.g. $$c \vert a$$ and $$c \vert b$$ then we say that c is a common divisor of a and b. For example, if we consider 10 and 15 then 5 divides both of them so 5 is a common divisor of 15 and 10.

We can then ask what is the biggest common divisor of two integer. We call this largest common divisor the greatest common divisor, often abbreviated to gcd. As an example, consider 12 and 18. 3 is a common divisor of both of them but its not the largest one. The largest one is 6 so we say the $$gcd(12, 18) = 6$$

# Lowest Common Multiples
Now let's talk about multiples. If I have some integer a and I multiply it by another integer b then $$ab$$ is a multiple of a (and b). So 12 is a multiple of 4 and 10 is a multiple of 5.

Given two integers a and b, if they're both multiples of c then we say c is a common multiple, for example 12 is a common multiple of 3 and 4.  We can then ask is there a smallest common multiple, we call this the lowest common multiple (abbreviated to lcm).

# Modular Arithmetic
Finally, let's talk about modular arithmetic. We can think of modular arithmetic as clock math. When we're telling the time when it gets around to 12 o'clock we don't go to 13 o'clock but rather we go back to 1 o'clock. Modular arithmetic is just an extension of this idea.

We start by picking some number, let's pick 3. Now when we're counting every time we should get to 3 we reset to 0. So first we get $$0, 1, 2$$ and instead of counting to 3 we reset so we get $$0, 1, 2, 0, 1, 2...$$

So now we can ask what happens when we add two numbers using this system. Well $$0 + 1 = 1$$ as normal and $$1 + 1 = 2$$ since we haven't got to 3 yet. But if what happens if we do $$2 + 1$$? We'll remember addition is really just moving us up the number line. So to add 1 to 2 we want to move up the number line 1 position and the number that comes after 2 is our new system is 0. 

To give you another example, in this system, $$2 + 2 = 4$$

We call this system addition mod 3 and we can do it for any other integer.

There is another way to think about this system which is to start again with number - let's pick 5 this time. And ask what is the remainder then we divide any number by it. For example, the remainder of 7 when we divide it by 5 is 2. We write this as $$7 \mod 5 = 2$$ Now for numbers less than 5 they stay unchanged since when we divide 4 by 5 we 0 remainder 4, so $$4 \mod 5 = 4$$. Note that $$5 \mod 5 = 0$$ since when we divide 5 by 5 we don't get a remainder.

Now, to do modular addition we just do the addition normally and then do the mod. For example $$8 + 3 \mod 5 = 11 \mod 5 = 1 \mod 5$$

In fact we can extend this to all other operations for example $$4 * 3 \mod 5 = 12 \mod 5 = 2 \mod 5$$

Now we're ready to dive into Shor's Algorithm.