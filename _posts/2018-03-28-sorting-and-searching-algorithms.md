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


#### Divide and Conquer (D&C)

To recap, here’s how D&C works:
1. Figure out a simple case as the base case.
2. Figure out how to reduce your problem and get to the base case.

Example:

Suppose you’re a farmer with a plot of land.
1680x640 meters

You want to divide this farm evenly into square plots. You want the plots to be as big as possible. 

1. Figure out the base case. This should be the simplest possible case. 
When the recursive function will end to call 
itself.

2. Divide or decrease your problem until it becomes the base case.


Suppose one side is 25 meters (m) and the other side is 50 m. Then the largest box you can use is 25 m × 25 m. You need two of those boxes to divide up the land.

> Euclid’s algorithm

> Sneak peak at functional programming

> Inductive proofs



1. Divide the problem into a number of subproblems that are smaller instances of the same problem.
2. Conquer the subproblems by solving them recursively. If they are small enough, solve the subproblems as base cases.
3. Combine the solutions to the subproblems into the solution for the original problem.

![Alt text](/techtalks/public/img/algorithms/divide_conquer.png?raw=true "Title")
![Alt text](/techtalks/public/img/algorithms/divide_conquer_example.png?raw=true "Title")


#### Average case vs. worst case


#### Traveling salesperson problem.


The salesperson has to go to five cities.
This salesperson, whom I’ll call Opus, wants to hit all five cities while
traveling the minimum distance.

5! = 120
There are 120 permutations with 5 cities,

In general, for n items, it will take n! (n factorial) operations to
compute the result. So this is O(n!) time, or factorial time


### Categories of algorithms 
Search 	− Algorithm to search an item in a data structure.
Sort 	− Algorithm to sort items in a certain order.
Insert 	− Algorithm to insert item in a data structure.
Update 	− Algorithm to update an existing item in a data structure.
Delete 	− Algorithm to delete an existing item from a data structure.


### Algorithm Complexity

Time Factor  − Time is measured by counting the number of key operations such as comparisons in the sorting 						algorithm.
Space Factor − Space is measured by counting the maximum memory space required by the algorithm.

#### Algorithm falls under three types 

Best Case 		− Minimum time required for program execution.
Average Case	− Average time required for program execution.
Worst Case 		− Maximum time required for program execution.

#### Common Asymptotic Notations

constant	−	Ο(1)
logarithmic	−	Ο(log n)
linear		−	Ο(n)
n log n		−	Ο(n log n)
quadratic	−	Ο(n2)
cubic		−	Ο(n3)
polynomial	−	nΟ(1)
exponential	−	2Ο(n)

### Greedy Algorithms

Greedy algorithms try to find a localized optimum solution, which may eventually lead to globally optimized solutions. However, generally greedy algorithms do not provide globally optimized solutions.

![Alt text](/techtalks/public/img/algorithms/greedy_algorithm_1.png?raw=true "Title")
![Alt text](/techtalks/public/img/algorithms/greedy_algorithm_2.png?raw=true "Title")

Most networking algorithms use the greedy approach. Here is a list of few of them −

Travelling Salesman Problem
Prim's Minimal Spanning Tree Algorithm
Kruskal's Minimal Spanning Tree Algorithm
Dijkstra's Minimal Spanning Tree Algorithm
Graph - Map Coloring
Graph - Vertex Cover
Knapsack Problem
Job Scheduling Problem



#### The Knapsack problem

#### The set-covering problem
Combinatorics

#### Approximation algorithms


### Dynamic Programming

Dynamic programming starts by solving subproblems and builds up to solving the big problem.


• Dynamic programming is useful when you’re trying to optimize something given a constraint. In the knapsack problem, you had to maximize the value of the goods you stole, constrained by the size of the knapsack.
• You can use dynamic programming when the problem can be broken into discrete subproblems, and they don’t depend on each other.

It can be hard to come up with a dynamic-programming solution. That’s what we’ll focus on in this section. Some general tips follow:

• Every dynamic-programming solution involves a grid.
• The values in the cells are usually what you’re trying to optimize.
For the knapsack problem, the values were the value of the goods.
• Each cell is a subproblem, so think about how you can divide
your problem into subproblems. That will help you figure out what
the axes are.


### The Feynman algorithm

#### Longest common subsequence

#### Longest common substring

#### Levenshtein distance

#### k-nearest neighbors

#####  Pythagorean formula

##### Cosine similarity

• KNN is used for classification and regression and involves looking
at the k-nearest neighbors.
• Classification = categorization into a group.
• Regression = predicting a response (like a number).


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



### Divide-and-conquer
The following computer algorithms are based on divide-and-conquer programming approach −

Merge Sort
Quick Sort
Binary Search
Strassen's Matrix Multiplication
Closest pair (points)

### Dynamic Programming

Dynamic programming approach is similar to divide and conquer in breaking down the problem into smaller and yet smaller possible sub-problems.

Dynamic programming is used where we have problems, which can be divided into similar sub-problems, so that their results can be re-used. Mostly, these algorithms are used for optimization. Before solving the in-hand sub-problem, dynamic algorithm will try to examine the results of the previously solved sub-problems. The solutions of sub-problems are combined in order to achieve the best solution.

The following computer problems can be solved using dynamic programming approach −

Fibonacci number series
Knapsack problem
Tower of Hanoi
All pair shortest path by Floyd-Warshall
Shortest path by Dijkstra
Project scheduling

Dynamic programming can be used in both top-down and bottom-up manner.



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

### Breadth-first search
The algorithm to solve a shortest-path problem is called breadth-first search.

Each graph is made up of nodes and edges.
(A) ---edge---> (B)
A and B are neighbors 

• Question type 1: Is there a path from node A to node B?
• Question type 2: What is the shortest path from node A to node B?



### Graphs



![Alt text](/techtalks/public/img/algorithms/connection_degree.png?raw=true "Title")
Directed graph—the relationship is only one way.


hash table allows you to map a key to a value

```
graph = {}
graph[“you”] = [“alice”, “bob”, “claire”]
graph[“bob”] = [“anuj”, “peggy”]
graph[“alice”] = [“peggy”]
graph[“claire”] = [“thom”, “jonny”]
graph[“anuj”] = []
graph[“peggy”] = []
graph[“thom”] = []
graph[“jonny”] = []
```

> A tree is a special type of graph, where no edges
ever point back.

## Graph Implementations

### Edge lists

One simple way to represent a graph is just a list, or array, of |E| ∣E∣vertical bar, E, vertical bar edges, which we call an edge list. To represent an edge, we just have an array of two vertex numbers, or an array of objects containing the vertex numbers of the vertices that the edges are incident on

![Alt text](/techtalks/public/img/algorithms/edge_list_example.png?raw=true "Title")

```
[ [0,1], [0,6], [0,8], [1,4], [1,6], [1,9], [2,4], [2,6], [3,4], [3,5],
[3,8], [4,5], [4,9], [7,8], [7,9] ]
```

### Adjacency Matrix

For a graph with |V| ∣V∣vertical bar, V, vertical bar vertices, an adjacency matrix is a |V| \times |V| ∣V∣×∣V∣vertical bar, V, vertical bar, times, vertical bar, V, vertical bar matrix of 0s and 1s, where the entry in row i ii and column j jj is 1 if and only if the edge (i,j) (i,j)left parenthesis, i, comma, j, right parenthesis is in the graph. 

![Alt text](/techtalks/public/img/algorithms/adjacency_matrix_example.png?raw=true "Title")

Directed Graph
	Unweighted graph boolean
	Weighted graph values

### Adjacency List

Representing a graph with adjacency lists combines adjacency matrices with edge lists. For each vertex i ii, store an array of the vertices adjacent to it. We typically have an array of |V| ∣V∣vertical bar, V, vertical bar adjacency lists, one adjacency list per vertex. 

![Alt text](/techtalks/public/img/algorithms/adjacency_list_example.png?raw=true "Title")

In JavaScript, we represent these adjacency lists by:
```
[ [1, 6, 8],
  [0, 4, 6, 9],
  [4, 6],
  [4, 5, 8],
  [1, 2, 3, 5, 9],
  [3, 4],
  [0, 1, 2],
  [8, 9],
  [0, 3, 7],
  [1, 4, 7] ]
 ```

## Graph Traversals

### Depth First Search (DFS) 

Depth First Search (DFS) algorithm traverses a graph in a depthward motion and uses a stack to remember to get the next vertex to start a search, when a dead end occurs in any iteration.

Rule 1 − Visit the adjacent unvisited vertex. Mark it as visited. Display it. Push it in a stack.
Rule 2 − If no adjacent vertex is found, pop up a vertex from the stack. (It will pop up all the vertices from the 
, which do not have adjacent vertices.)
Rule 3 − Repeat Rule 1 and Rule 2 until the stack is empty.

### Breadth First Search (BFS)

Breadth First Search (BFS) algorithm traverses a graph in a breadthward motion and uses a queue to remember to get the next vertex to start a search, when a dead end occurs in any iteration.


Rule 1 − Visit the adjacent unvisited vertex. Mark it as visited. Display it. Insert it in a queue.
Rule 2 − If no adjacent vertex is found, remove the first vertex from the queue.
Rule 3 − Repeat Rule 1 and Rule 2 until the queue is empty.

### Dijkstra’s algorithm

## Tree
Tree represents the nodes connected by edges. 

![Alt text](/techtalks/public/img/algorithms/binary_tree.jpg?raw=true "Title")

every tree have n nodes n-1 edges

### Binary Search Tree

A Binary Search Tree (BST) is a tree in which all the nodes follow the below-mentioned properties −

The left sub-tree of a node has a key less than or equal to its parent node's key.

The right sub-tree of a node has a key greater than to its parent node's key.