---
author: teymur
comments: true
date: 2018-03-17 22:16:08+00:00
layout: post
slug: arithmetic-sets
title: Arithmetic Sets
categories: Tutorial
tags:
- math
---


> Set is collection of distinct objects

	∅ - is null set


## Membership
```
A = {1,2,3,4}
4 ∈ A 
9 ∉ A 
```

## Equality
```
A is {1, 2, 3}
B is {3, 1, 2}

A = B
```
## Unions
Two sets can be "added" together. The union of A and B, denoted by A ∪ B, is the set of all things that are members of either A or B.
```
{1, 2} ∪ {1, 2} = {1, 2}
{1, 2} ∪ {2, 3} = {1, 2, 3}
{1, 2, 3} ∪ {3, 4, 5} = {1, 2, 3, 4, 5}
```
## Intersections
```
{1, 2} ∩ {1, 2} = {1, 2}
{1, 2} ∩ {2, 3} = {2}
```
## Complements

Two sets can also be "subtracted". The relative complement of B in A (also called the set-theoretic difference of A and B), denoted by A \ B (or A − B)
```
A′ = U \ A

{1, 2} \ {1, 2} = ∅.
{1, 2, 3, 4} \ {1, 3} = {2, 4}.

A \ B ≠ B \ A  for A ≠ B.

```
## Universal set and absolute complement
```
U  - Universal set
A′ - All things in the universe that are not in A

A′ = U \ A = U - A

C = {0,5,15,3}

0 ∈ C 
12 ∉ C

C′ = U\C = U-C

0 ∉ C′ 
12 ∈ C′
```
## Subsets

If every member of set A is also a member of set B, then A is said to be a subset of B, written A ⊆ B (also pronounced A is contained in B). Equivalently, we can write B ⊇ A, read as B is a superset of A, B includes A, or B contains A. The relationship between sets established by ⊆ is called inclusion or containment.

subset of this is {1, 2, 3}. Another subset is {3, 4} or even another is {1}, etc.
```
{1, 3} ⊆ {1, 2, 3, 4}.
{1, 2, 3, 4} ⊆ {1, 2, 3, 4}.
```

The empty set is a subset of every set and every set is a subset of itself:
```
∅ ⊆ A.
A ⊆ A.
```
Every set is a subset of the universal set:
```
A ⊆ U.
```

	number of subset of set is 2^n
	n is number of elements

### Proper Subsets (strict subsets)

If A is a subset of, but not equal to, B, then A is called a proper subset of B, 
written A ⊊ B (A is a proper subset of B) or B ⊋ A (B is a proper superset of A).

```
{1, 2, 3} is a subset of {1, 2, 3}, 
but is not a proper subset of {1, 2, 3}.

{1, 2, 3} is a proper subset of {1, 2, 3, 4}
because the element 4 is not in the first set.

{1, 2, 3, 4}  is a proper superset of {1, 2, 3}

{1, 2, 3} ⊆ {1, 2, 3}
{1, 2, 3} ⊊ {1, 2, 3, 4} we can say {1, 2, 3} ⊆ {1, 2, 3, 4}
{1, 2, 3, 4} ⊋ {1, 2, 3} 
```

### Posibile Subset
```
{1, 2, 3}
subsets
{} or ∅,{1},{2},{3},{1,2},{1,3},{2,3},{1, 2, 3}
```

## References
* [https://en.wikipedia.org/wiki/Set_(mathematics)/](https://en.wikipedia.org/wiki/Set_(mathematics))
