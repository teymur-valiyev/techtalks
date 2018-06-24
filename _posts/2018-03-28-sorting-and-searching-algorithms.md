---
author: teymur
comments: true
date: 2018-03-25 00:00:00+00:00
layout: post
slug: sorting-and-searching-algorithms
title: Sorting and Searching Algorithms
categories: Tutorial
tags:
- computer-science
- algorithms
- sort-algorithms
- search-algorithms
---


## Sorting algorithms
Classification 
	1. Time complexity
	2. Space Complexity or Memory usage
		* Inplace, Constant memory
		* Memory usage grow with input size
	3. Stability
	4. Internal Sort vs External sort
		internal sort all records ram
		external sort recorts are on disk
	5. Recurive or non-recursive

### Selection sort

The smallest element is selected from the unsorted array and swapped with the leftmost element, and that element becomes a part of the sorted array. This process continues moving unsorted array boundary by one element to the right.

average and worst case complexities are of Ο(n2), where n is the number of items.


### Selection sort

Example:
Suppose you have a bunch of music on your computer.
For each artist, you have a play count.


One way is to go through the list and find the most-played artist. Add that artist to a new list.

Keep doing this, and you’ll end up with a sorted list.

You check n elements, then n – 1, n - 2 ... 2, 1. On average, you check a
list that has 1 / 2 × n elements. The runtime is O(n × 1 / 2 × n). But constants
like 1 / 2 are ignored in Big O notation (again, see chapter 4 for the full
discussion), so you just write O(n × n) or O(n 2 ).
This takes O(n×n) time or O(n^2) time.

very recursive function has two parts: the base
case, and the recursive case. The recursive case is when the function calls
itself. The base case is when the function doesn’t call itself again ... so it doesn’t go into an infinite loop.



### Bubble sort

This sorting algorithm is comparison-based algorithm in which each pair of adjacent elements is compared and the elements are swapped if they are not in order. This algorithm is not suitable for large data sets as its average and worst case complex 

average and worst case complexity are of Ο(n2) where n is the number of items.

### Insertion Sort

The array is searched sequentially and unsorted items are moved and inserted into the sorted sub-list (in the same array)

average and worst case complexity are of Ο(n2), where n is the number of items.



### Merge sort

Merge sort is a sorting technique based on divide and conquer technique. With worst-case time complexity being Ο(n log n), it is one of the most respected algorithms.

Merge sort first divides the array into equal halves and then combines them in a sorted manner.

Divide array to arrays and achieve atomic value which can no more be divided.
Now, we combine them in exactly the same manner as they were broken down

### Quicksort sort 

in-place memory 

average-case time complexity 	O(nlogn) 
worst case time complexity 		O(n^2)





## Binary search

With binary search, you guess the middle number and eliminate half the remaining numbers every time


#### Example 
The dictionary has 240,000 words.
Simple search could take 240,000 steps

Binary search you cut the number of words in half until you’re left with only one word. So binary search will take 18 steps

Simple search will take n steps.
Binary search will take log2n steps to run in the worst case.

Binary search only works when your list is in sorted order

log10 100 is like asking, “How many 10s do we multiply together to get 100?” 
The answer is 2: 10 × 10.

Logs are the flip of exponentials.


If this is a list of 100 numbers, it takes up to 100 guesses.
If it’s a list of 4 billion numbers, it takes up to 4 billion guesses. So the
maximum number of guesses is the same as the size of the list. This is
called linear time.


Binary search is different. If the list is 100 items long, it takes at most
7 guesses. If the list is 4 billion items, it takes at most 32 guesses.
Powerful, eh? Binary search runs in logarithmic tim

Simple searche - O(n)
Binary search -  O(logn)

Big O notation lets you compare the number of operations. It tells you how fast the algorithm grows.


Big O establishes a worst-case run time

#### Some common Big O run times

• O(log n), also known as log time. Example: Binary search.
• O(n), also known as linear time. Example: Simple search.
• O(n * log n). Example: A fast sorting algorithm, like quicksort
(coming up in chapter 4).
• O(n 2 ). Example: A slow sorting algorithm, like selection sort
(coming up in chapter 2).
• O(n!). Example: A really slow algorithm, like the traveling
salesperson (coming up next!).


Suppose you’re drawing a grid of 16 boxes again, and you can choose
from 5 different algorithms to do so. If you use the first algorithm, it
will take you O(log n) time to draw the grid. You can do 10 operations 
per second. With O(log n) time, it will take you 4 operations to draw a
grid of 16 boxes (log 16 is 4). So it will take you 0.4 seconds to draw
the grid. What if you have to draw 1,024 boxes? It will take you
log 1,024 = 10 operations, or 1 second to draw a grid of 1,024 boxes.
These numbers are using the first algorithm.


• Algorithm speed isn’t measured in seconds, but in growth of the
number of operations.
• Instead, we talk about how quickly the run time of an algorithm
increases as the size of the input increases.
• Run time of algorithms is expressed in Big O notation.
• O(log n) is faster than O(n), but it gets a lot faster as the list of items
you’re searching grows.

Array reading 	O(1)
Array insertion O(n)
Array Delete 	O(n)
Lists reading 	O(n)
Lists Insertion O(1)
Lists Insertion O(1)

There are two different types of access: random access and sequential access.	


Linked lists are good for inserts/deletes, and arrays are good for random access.

Let’s consider a hybrid data structure: an array
of linked lists. You have an array with 26 slots. Each slot points to a
linked list. For example, the first slot in the array points to a linked
list containing all the usernames starting with a. The second slot
points to a linked list containing all the usernames starting with b,
and so on.




#### Traveling salesperson problem.


The salesperson has to go to five cities.
This salesperson, whom I’ll call Opus, wants to hit all five cities while
traveling the minimum distance.

5! = 120
There are 120 permutations with 5 cities,

In general, for n items, it will take n! (n factorial) operations to
compute the result. So this is O(n!) time, or factorial time




### Tree 

### Binary search tree

• B-trees
• Red-black trees
• Heaps
• Splay trees

### Inverted indexes

### The Fourier transform

### Parallel algorithms

## MapReduce

### Distributed algorithm





### Interpolation Search

### Hash Table




#### Collisions

To avoid collisions, you need
• A low load factor
• A good hash function

##### Load factor

number of items in hash table / total number of slots

2/5 = 0.4

Suppose you need to store the price of 100 produce items in your hash table, and your hash table has 100 slots. In the best case, each item will get its own slot.
This hash table has a load factor of 1

Once the load factor starts to grow, you need to add more slots to your hash table. This is called resizing.

array size 4 load factor - 4/3
resize hash table 
array size 8 load factor - 8/3

“This resizing business takes a lot of time!” And
you’re right. Resizing is expensive, and you don’t want to resize too often. But averaged out, hash tables take O(1) even with resizing.


A good hash function distributes values in the array evenly.
A bad hash function groups values together and produces a lot of collisions.

