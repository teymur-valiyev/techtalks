---
author: teymur
comments: true
date: 2018-04-01 00:00:00+00:00
layout: post
slug: graph-theory
title: Graph theory
categories: Tutorial
tags:
- graph
- computer-science
- algorithms
- data-structure
---

**The Graph** is similar to the Tree. The difference is that there’s no
children or parent nodes, and therefore, no Root Node.
For example, graphs are ideal for representing a social network, where nodes are people and edges represent friendships.


https://medium.com/basecs/from-theory-to-practice-representing-graphs-cfd782c5be38

## Types of Graphs

* Undirected Graph - A undirected graph contains edges but the edges are not directed ones.
* Directed Graph - In a directed graph, each edge has a direction.
* Weighted Graphs - edges has weight to represent an value

## Rerpresenting Graphs

https://visualgo.net/en/graphds

### Edge lists

One simple way to represent a graph is just a list, or array
![Alt text](/techtalks/public/img/algorithms/edge_list_example.png?raw=true "Title")

```
[ [0,1], [0,6], [0,8], [1,4], [1,6], [1,9], [2,4], [2,6], [3,4], [3,5],
[3,8], [4,5], [4,9], [7,8], [7,9] ]
```

### Adjacency Matrix

An adjacency matrix is a square matrix used to represent a finite graph. The elements of the matrix indicate whether pairs of vertices are adjacent or not in the graph.
If the value is 1, that means that there is an edge between the two nodes; if the value is 0, that means an edge does not exist between them.

![Alt text](/techtalks/public/img/algorithms/adjacency_matrix_example.png?raw=true "Title")

![Alt text](/techtalks/public/img/datastructure/adjacency-matrix.png?raw=true "an adjacency matrix")

The interesting thing about adjacency matrix representations of a graph is that, just by looking at them, we can tell whether the graph is directed or undirected. We can determine this characteristic of a graph based on whether its adjacency matrix is symmetric or not. If the values on both sides of the main diagonal of an adjacency matrix are the same, the matrix is symmetric. 


### Adjacency List

Representing a graph with adjacency lists combines adjacency matrixes with edge lists. 
An adjacency list is an array of linked lists that serves as a representation of a graph.

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


## Directed graph
Directed graph—the relationship is only one way.

![Alt text](/techtalks/public/img/algorithms/connection_degree.png?raw=true "Title")

Hash table allows you to map a key to a value
 
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

## Graph Traversals

## Depth First Search (DFS) 

The DFS algorithm is a recursive algorithm that uses the idea of backtracking.

DFS algorithm traverses a graph in a depthward motion and uses a stack to remember to get the next vertex to start a search, when a dead end occurs in any iteration.


* Rule 1 − Visit the adjacent unvisited vertex. Mark it as visited. Display it. Push it in a stack.
* Rule 2 − If no adjacent vertex is found, pop up a vertex from the stack. (It will pop up all the vertices from the 
, which do not have adjacent vertices.)
* Rule 3 − Repeat Rule 1 and Rule 2 until the stack is empty.

Time Comlexity O(V+E) - Vertices(nodes) + Edges(links)

* Minimum Spanning Tree
* Detect and find cycles in a graph
* Check if a graph is bipartite
* Find strongly connected components
* Topologically sort the nodes of a graph
* Find bridges and articution points
* Find augmenting paths in a flow netword 
* Generate mazes

### Minimum Spanning Tree

Spanning Tree is subset of edges that connects all vertices. 
Minimum spanning tree is the spanning tree where the cost is minimum among all the spanning trees.

![Alt text](/techtalks/public/img/algorithms/minimum_spanning_tree.jpg?raw=true "Minimum Spanning Tree")

Algorithms for finding the Minimum Spanning Tree:
* Kruskal’s Algorithm
* Prim’s Algorithm

### Topological Sort

## Breadth First Search (BFS)


The BFS algorithm starts at the tree root and explores the neighbor nodes first, before moving to the next level neighbours. 


BFS algorithm traverses a graph in a breadthward motion and uses a <a href="{{ site.baseurl }}{{ BASE_PATH }}/2018/03/27/data-structure#queue" target="_blank" >queue</a>
 to remember to get the next vertex to start a search, when a dead end occurs in any iteration.

* Rule 1 − Visit the adjacent unvisited vertex. Mark it as visited. Display it. Insert it in a queue.
* Rule 2 − If no adjacent vertex is found, remove the first vertex from the queue.
* Rule 3 − Repeat Rule 1 and Rule 2 until the queue is empty.

Time Comlexity O(V+E) - Vertices(nodes) + Edges(links)

--------------------------

### Directed acyclic graph (DAG)

A directed acyclic graph is a finite directed graph with no directed cycles. 


--------------------------
### Graph Theory Problems

Shortest Path Problem
* BFC (unweighted graph)
* Dijkstars 
* Bellman-Ford 
* Floyd-Warshall
* A*
etc.. 

Connectivity
* DFC

Negative cycles
* Bellman-Ford
* Floyd-Warshall

Strongly Connected Components
* Tarjans 
* Kosaraju 

Traveling Salesman Problem
* Help-Karp
* Brand and Bound
* approximation algorithms

Bridges
Articulation points
* DFS 

Minimal Spanning Tree (MST)
* Kruskals
* Prims & Boravks 

Network flow: max flow
* Ford-Fulkerson
* Edmonds-Karp & Dinic




--------------------------

## Tree

A tree in an undirectect graph with no cycles. Tree represents the nodes connected by edges. 

![Alt text](/techtalks/public/img/algorithms/binary_tree.jpg?raw=true "Title")

> Every tree have n nodes(vertices) n-1 edges


----------------------------------------------------




-------------------------------------------------








## Binary Search Tree

A Binary Search Tree (BST) is a tree in which all the nodes follow the below-mentioned properties −

The left sub-tree of a node has a key less than or equal to its parent node's key.

The right sub-tree of a node has a key greater than to its parent node's key.



## Dijkstra’s algorithm



https://www.khanacademy.org/computing/computer-science/algorithms/graph-representation/a/representing-graphs

https://www.hackerearth.com/practice/algorithms/graphs/minimum-spanning-tree/tutorial/