---
layout: post
title: An Introduction to de Sitter Space - Part 1
author: Charles Thomas
---

Most of my work is on a spacetime called de Sitter space, so I wanted to write a series explaining what that actually is and why it is interesting. So let's dive in.

# What is a spacetime?
A spacetime is the arena in which physics takes place. Prior to Einstein, we usually took it be $$\mathbb{R}^4$$ - this means to specify a point in space and time we need 4 numbers: the x, y, and z positions and then the time t. Then if someone gives us two points in spacetime $$(x,y,z,t)$$ and $$(x',y',z', t')$$ then the distance between them is $$\sqrt{tt' + xx' + yy' + zz'}$$

In 1905 with the advent of Special Relativity, we learnt that spacetime should be be $$\mathbb{R}^{1,3}$$. What is means is we still we need to 4 numbers to describe a point in spacetime but now the 'distance' between $$(x,y,z,t)$$ and $$(x',y',z', t')$$ is $$\sqrt{ - tt' + xx' + yy' + zz'}$$ (it's not obvious but this is a consequence of the speed of light being constant).

Then roughly 10 years later, Einstein told us spacetime is more general than this, it is a 4D Lorentzian manifold. 

A manifold is a space that if you look close enough at any point the space look flat. To give some intuition for this, we live on the surface of the earth, we known the earth is round but in our day to day lives we don't notice this. This is because we are so small relatively to the Earth that is appears flat.

Now a 4D Lorentzian manifold is a space that on small small scales looks like $$\mathbb{R}^{1,3}$$.  This means the universe might be curved in general but we're just too small to notice.

For the more mathematically minded people, spacetime is a 4D manifold with a (psuedo)-metric e.g. a metric that is everywhere non-degenerate (but not necessarily positive definite) with signature (1, 3).

# What is curvature?
We said that spacetime might be curved but what do we mean by this? Let's start with some simple examples. A piece of paper is flat so we say it has no curvature. Now imagine a sphere and a pringle. They're both curved but in different ways. On a sphere no matter which direction you move you'll always be curving in the same direction. Where as on a pringle, if you move one way you'll be curving upwards but if you move in a different direction you'll be curving downwards. To distinguish between these two cases we say a sphere is positively curved and a pringle is negatively curved.

Mathematically, we describe the curvature of a manifold using an object called the Riemann curvature tensor $$R_{\mu\nu\rho\sigma}$$. This captures the full information about the curvature of the manifold but we can build simpler objects that only capture some of information about the curvature of the object. These are the Ricci curvature tensor $$R_{\mu\nu}$$ and the Ricci scalar $$R$$.


# Einstein Equations
Einstein actually told us that spacetime can't just be any 4D Lorentzian manifold but instead it must obey certain constraints. Specifically, the metric (the mathematical object used for computing distances) must obey the following equation:

\begin{equation}
    R_{\mu\nu} - \frac{1}{2}Rg_{\mu\nu} + \Lambda g_{\mu\nu} = \kappa T_{\mu\nu}
\end{equation}

This equation relates the metric and the curvature on the left hand side to this object called $$T_{\mu\nu}$$. This is called the energy momentum tensor and it describes how matter is distributed in the universe.

What this means is that how curved space is depends on how energy and matter (e.g. stuff) is distributed in the universe. In particular, if I have lots of mass or energy in one place then the universe will be very curved.

Finding solutions to this is hard and not many exact solutions are known. However, the few that are known are very useful, for example, the Schwarzschild solution predicts black holes. 

de Sitter space is one solution to these equations and it's special because it is one of the 'maximally symmetric' spacetimes. I'll try to explain what this means in the next post.