---
layout: post
title: DNA Sequencing
author: Charles Thomas
---

Plan:
* DNA is made up of two chains arranged in a double helix
* Each chain made up on of four molecules (nucleotides): cytosine [C], guanine [G], adenine [A] or thymine [T]
* DNA sequencing aims to work out what order these are in a chain
* DNA chains are too long to sequence the whole thing
* So broken up into smaller fragments, often at random (shotgun sequencing)
* We then need to piece these fragments together
* Each fragment overlaps with each other (mer)
* If each fragment is 3 molecules e.g. CTG, AGT etc.
* We can phrase this problem as a graph theory problem

Graph Theory:
* What's a graph?
* What's a directed graph?
* What's a path?
* What's a Hamiltonian path
* What's a Eulerian path
* What's a (semi)-Eulerian graph

Hamiltonian
* Give each fragment a node
* Consider two nodes A & B: There is an edge from node A to if the last two characters of A are the same as the first two characters as B
* So CTG would have edges to TGA or TGC etc.
* Now if we find a path that visits every node exactly once we will (Hamiltonian) have constructed the DNA sequence
* This NP-complete (explain this)


Eulerian 
* Phrase problem another way
* For each fragment split it into the first two characters and the last two characters; these become nodes
* So CTG becomes nodes CT and TG
* Edges between two nodes if the last characters of node A is the same as the first character of node B so CT joins to TG and TG joins to GA
* Now each edge represents a fragment: the edge between CT and TG represents the fragment CTG
* This is actually a type of construction known as a De Brujin graph
* If we find a path that visits every edge once (Eulerian) we will have constructed the whole sequence
* We can do this in linear time using Hierholzer's algorithm

Hierholzer's algorithm
* Have to make sure graph is Eulerian or semi-Eulerian
* Start a vertex v
* Randomly choose unvisted from edge from v 
* Repeat until returning to v
* While there is a vertex u in the current tour that has unvisted edges then create cycle from there
