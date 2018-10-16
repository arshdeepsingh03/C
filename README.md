# CPEN 221 - Fall 2018 - MP2
# Preliminary Design Discussion

## Students (name, student number, github username)
1. Arshdeep Singh Sandhu, 57198574 arshdeepsingh03
2. Xianda Sun, 43409804, michael33sun

## How do the adjacency list and adjacency matrix representation differ from each other? How will you implement these representations in Java for MP2? Notice that you cannot make assumptions about graph size ahead of time.

In adjacency list representation,
1. We maintain a list of vertices adjacent to a given vertex for each vertex in G = (V, E)
2. These <Vertex, List<Vertex>> pairs can be stored in a HashMap for quick access.
3. It is convenient to discover the neighbours of any vertex using these lists.

In the matrix representation, 
1. We maintain a n X n matrix of boolean values where n is the current number of nodes in the graph. 
2. It is very convenient to discover if 2 vertices are adjacent.
3. This behaviour can be implemented using a nested HashMap as described: For each vertex V in G, we maintain a HashMap containing all vertices in G (including V) mapped to a Boolean value. This boolean value would indicate if the vertices are connected or not. Interestingly, all these HashMaps can be stored in another HashMap for quick access.
4. We also need to maintain a set of vertices that are currently present in the graph, as vertices are key values for hashmap and cannot be recovered once inserted into the HashMap.

*Note: both of these implementations can grow dynamically!*
	
## What is breadth first search on a graph? Construct a small graph (8-12 vertices and 16-20 edges) and illustrate the outcome from performing a BFS on this graph. You must indicate the output in a manner that is consistent with what is expected of the BFS implementation for this assignment.

The breadth first search algorithm traverses the graph starting from a node in the breadth first fashion i.e. 
1. first a random node is selected.
2. All nodes that are adjacent to this node are marked as visited.
3. All nodes adjacent to nodes in 2 that have not yet been visited are marked as visited.
4. The process is continued until all nodes are visited!

2 images at the end of this document show this process stepwise.

## State the representation invariant for the adjacency matrix implementation of the `Graph` interface.

In abstract terms, for a matrix representation, we need a n X n matrix of boolean values, where n is the number of vertices in graph. For Example, the following would be a representaion for a graph with 2 vertices that are connected together:

V1	V2
0	1	V1
1	0	V2

By careful examination, we conclude that, this matrix must have *ALL* of the following properties to be a valid representation described in the graph interface specifications:

P1: The matrix is square. Note: The size can be 0 X 0 for empty, newly initialized graphs.
P2. The diagonal elements must be zero to avoid self loops
P3: The matrix should be symmetric along the principal diagonal. i.e. matrix(i,j) = matrix(j,i) for all 0 <= i,j < n, where n is the size of the matrix.

*The representation invariant is therefore P1 ^ P2 ^ P3 = true, where ^ denotes logical AND.*
In terms of our specific matrix implementation (There can be various others), these conditions can be easily maintained.

## How will you strengthen the specification for the `addVertex` method when compared with the specification that is part of the `Graph` interface?

In order to strengthen the addVertex specification, we can weaken the precondition so that it accepts any non-null vertex, even if its already in the graph, and, we can strengthen the postcontion and return a boolean value as an indicator as to the success of an addition.
More precisely, 

/**
     * Adds a vertex v to graph.
     * @param: v is not null
     * @return: true if addition was successful
     		false if v is already in the graph.
     */
public boolean addVertex(Vertex v);

## Write a test case for the `center` method in Algorithms. Your test case must involve a graph with 6-8 vertices and 15-18 edges.

We test a very special case here! A *complete graph with 6 vertices and 6 X 5 / 2 = 15 edges!* In this case, any vertex could be a valid center as all vertices are equivalent. We believe that this makes this case as an ideal test case to look for infinite loops etc in the code. Of course, more test cases will be discovered later on.

