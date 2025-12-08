---
layout: post
title: An Introduction to de Sitter Space - Part 2
author: Charles Thomas
---

Last time, we explored the ideas of spacetime and curvature. This time we'll look at some special spacetimes: the maximally symmetric spacetimes.


# Isometries
One important class of solutions to the Einstein equations is the maximally symmetric solutions - that is the solutions that in some sense have the most symmetry. To get some intuition, imagine a ball, this seems to have a lot of symmetry as I can rotate it in lots of different ways and it looks the same. But if the ball had a bump somewhere it would be a lot less symmetric.

To make this more formal, let us consider two manifolds with metrics (distance measuring functions), formally called Riemannian manifolds. $$(M,g)$$ and $$(N, h)$$. A symmetry will be some function $$f: M \to N$$ that relates the two manifolds. But it should also have some nice properties for us to consider it a symmetry. Firstly, it should be invertible (e.g. we should be able to undo it) which makes sense as if we have symmetry sending us from M to N, we should have a symmetry going from N to M. We call the inverse map $$f^{-1}$$. 

Secondly, it should be continuously differentiable. For the non-mathematically minded people this means the function shouldn't have any jumps - it should send nearby inputs to nearby outputs (one way people think about it is that if we drew the function then we could do it without picking up our pen). The term for a function which satisfies these first two properties is a diffeomorphism.

Finally, we need this map to relate the two metrics  on M and N.  In particular, we want that for every pair of points u and v 

\begin{equation}
    g(u, v) = h(f(u), f(v))
\end{equation}

e.g. the symmetry doesn't change the distance between two points. We can express this requirement in terms of the pullback as $$f^* g = h$$ (don't worry if you haven't come across pullbacks before).

So putting this together we call a function that is a diffeomorphism satisfying $$f^* g = h$$ a symmetry or more properly an isometry (and we usually take M to the same as N).

If we have two isometries then we can combine them together to get a third isometry by doing one then the other. This means the isometries of a manifold form a group (a special kind of mathematical object) which we call the isometry group. In fact, the isometry is a special kind of group called a Lie group (and has a maximum dimension of n(n+1)/2).

# Killing Vector Fields
A vector field is informally an assignment of a vector to every point in space (pedantically, it is a smooth section of the tangent bundle). Think about there being a little arrow at every point in space. 

We call a vector field, X, a Killing vector field if it obeys

\begin{equation}
    \mathcal{L}_Xg = 0
\end{equation}

What this means is if we follow the vector field (imagine starting at some point then follow the little arrow to a nearby point, then follow the little arrow at this new point to another point and so on), then as we do this the metric doesn't change. The collection of Killing vector fields form a structure called a Lie algebra. 

Then it turns out the Lie algebra of complete (defined everywhere) Killing vector fields is a isomorphic (for the non mathematically minded this roughly means the same as) to the Lie algebra of the isometry group.

Practically, this means you can study the isometries of a manifold by instead studying its complete Killing vector fields (e.g. if you want to study the symmetries of a manifold you only need to study these special vector fields which is often easier mathematically).

To be more technical, on a manifold you have geodesics (roughly, these are curves which the shortest path between two points). Then if you have a geodesically complete manifold - that is a manifold where any geodesic can be extended infinitely, then every Killing vector field is complete so you can just study the Killing vector fields.

# Maximally symmetric spaces
We say a spacetime is maximally symmetric if it has two properties: homogeneity and isotropy.

Homogeneity says no point is more special than any others . This means there is no distinguished point, such as a centre. Mathematically, this means for any two points p and q there is an isometry sending p to q.

Isometry says there is no preferred direction in space - so whatever direction you look in space is the same. That means mathematically, given any point p and two tangent vectors v and w in $$T_pM$$ then there is an isometry such that induced map on the tangent space sends v to w.

If a manifold has these two properties then it is complete which means it has to have the maximal number of Killing vector fields: $$n(n+1)/2$$ where n is the dimension of spacetime.

This can be used to show that a maximally symmetric spacetime has constant Ricci scalar curvature R (this was an object that encodes some of the information about the curvature of manifold).

So  there are 3 types of maximally symmetric spacetimes: flat space (R=0), de Sitter space $$(R>0)$$ and anti de Sitter space $$(R < 0)$$ (technically, we can allow covers of these spaces due to centres in the isometry group that don't appear in the Lie algebra).