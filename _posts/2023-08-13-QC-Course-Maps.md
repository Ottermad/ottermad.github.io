---
layout: post
title: Basic Mathematics For Quantum Mechanics - Maps
author: Charles Thomas
---

## What is a map?
A map is a way of relating items in one set to items in another set. If we have a map called f from set A to set B we write:

$$f : A \rightarrow B$$

Let's see an example. If we have the sets

$$A = \{1, 2, 3\}$$

$$B = \{4, 5, 6\}$$

Then we can define the map

$$f : A \rightarrow B$$

$$f(x) = x + 3$$

So 

$$f(2) = 2 + 3 = 5$$

## Domains, Codomain and Range
The domain of a map is the set the map goes from and the codomain is the set it goes to. So if we have 

$$f : A \rightarrow B$$

Then A is the domain and B is the codomain

The range of a function is the set of all the outputs of a function. This sounds very similar to the codomain but it is different. To see this let's look at an example. If we have the following map:

$$g : \mathbb{Z} \rightarrow \mathbb{Z}$$

$$g(x) = x^2$$

Then the domain and the codomain are the set of integers. However, any integer squared is always positive so the range of the function is just the positive integers. So -1 is in the codomain but not in the range.

## Injective maps
Some maps are called 'injective' or 'one-to-one'. An injective map is one where no two inputs have the same output. Consider:

$$f : \{1, 2, 3\} \rightarrow \{12, 15, 16\}$$

$$f(1) = 12$$

$$f(2) = 16$$

$$f(3) = 15$$

This is an injective map because every input goes to a different output. But

$$f : \{1, 2, 3\} \rightarrow \{12, 15, 16\}$$

$$f(1) = 12$$

$$f(2) = 16$$

$$f(3) = 16$$

is not injective because 2 and 3 both go the same output.

When a map is injective, every output (e.g. everything in the range) has a unique inverse - we can tell exactly what the input was just from looking at the output.

## Surjective maps
Surjective maps are also called 'onto' maps. A surjective map is one where the co-domain is the same as the range - this means the function produces every possible output.

For example:

$$g : \mathbb{Z} \rightarrow \mathbb{Z}$$

$$g(x) = x^2$$

is not surjective as it will never produce -1.

But 

For example:

$$h : \mathbb{Z} \rightarrow \mathbb{Z}$$

$$h(x) = h + 3$$

is surjective as it will produce all the possible outputs e.g. all of the integers.

## Bijective maps
Some maps are both injective and surjective so we call these maps bijective. Sometimes you'll hear these maps called a bijection.

## Binary operations
Some maps can take more than one input. For example, addition is an example of a map that takes two inputs and gives us back a single output

A map f from two sets A and B to a third C is written like this:

$$f : A \times B \rightarrow C$$

For example we might have the map

$$f : \mathbb{R} \times mathbb{R} \rightarrow \mathbb{R}$$

$$f(x, y) = x + y + 2$$

A map can take any number of inputs but if it takes two inputs we call it a binary operation
