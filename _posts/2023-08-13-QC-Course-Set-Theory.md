---
layout: post
title: Basic Mathematics For Quantum Mechanics - Set theory
author: Charles Thomas
---

## What is a set?
A set is a collection of objects. We denote a set by putting the list of objects in curly brackets. Here are some examples:

$$\{1, 2, 4\}, \{cat, dog, bird\}, \{a, b, c\}$$

Note that sets do not have duplicate items.

Two sets are the same when they contain exactly the same objects. For example

$$\{a, b, c\} = \{c, a, b\}$$

Because they contain the same objects even though we've written them in a different order. But

$$\{a, b, c\} \neq \{a, b\}$$

Because c is one set but not the other.

## Combining Sets
There are two basic ways of making sets out of old ones.

Firstly, we can take the union (or more) of two sets. This is denoted by the symbol:

$$\cup$$

The union of two sets is a set with all the elements from either set. For example: 

$$\{1, 2, 3\} \cup \{4, 5, 6\} = \{1, 2, 3,4, 5,6\}$$

If an element is in both sets when we take the union that element only appears once because sets do not have duplicate items 

$$\{1, 2, 3\} \cup \{3, 4, 5\} = \{1, 2, 3, 4, 5\}$$ 

The second way of combining sets is the intersection, denoted by

$$\cap$$

The intersection of two sets is a set containing only the elements that were in both sets. For example:

$$\{1, 2, 3\} \cap \{3, 4, 5\} = \{3\}$$ 


## Subsets
Suppose we have two sets called A and B. If all the elements of set A are in set B then we say A is a subset of B and we write:

$$A \subseteq B$$

Let's look at an example

$$\{1, 2, 3\} \subseteq \{1, 2, 3, 4\}$$

Since all the elements in the set on the left are in the set on the right. In fact, a set is a subset of itself:

$$\{1, 2, 3, 4\} \subseteq \{1, 2, 3, 4\}$$

Because all the elements on the left are in the set on the right

Sometimes we want to discount the possibility of a subset being the same as the parent set e.g. we want the subset to be smaller.

In the case where we are only interested in subsets which are different from the parent set we write:

$$A \subset B$$

and we say A is a strict subset of B


## Sizes of sets
The size of a set is called its cardinality. For finite sets, it is the number of elements in that set. For infinite sets, it gets more complicated but that's a topic for another post.

We denote the size of a set with pipes e.g.

$$|\{a, b, c\}| = 3$$

## Useful sets to know
The empty set is the set with no elements in it. It is often denoted:

$$\varnothing$$

The natural numbers are the set of positive whole numbers (some authors choose to include 0, others do not). It is denoted:

$$\mathbb{N}$$

The integers are the set of whole numbers, denoted:

$$\mathbb{Z}$$

Finally, the real numbers are all the numbers we usually think of including irrational numbers like pi. We denote it:

$$\mathbb{R}$$