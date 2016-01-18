Lab Week 9: Graphs
==================

Graphs are defined as consisting of a set `V` of vertices
and a set `E` of edges. Edges are further defined as being
either an ordered pair of vertices (in the case of a directed
graph), or an unordered pair (in the case of an undirected
graph).

Implementation
--------------

The two primary ways that graphs are implemented are as an
adjacency matrix or as an adjacency list. An adjacency matrix
consists of a two dimensional array where the indices map to
the vertices and the intersections between every pair of vertices
indicate whether there is an edge connecting them and if so
what the weight of that edge is (in the case of a weighted
graph). The image below should help to illustrate this.

<img src="http://rosemary.umw.edu/~finlayson/class/spring13/cpsc230/notes/images/matrix.png"/>

This class definition should help give you an idea of where to
start when implementing a graph as an adjacency matrix.

```cpp
class AdjacencyMatrix{
    private:
        int n;
        int **adj;
        bool *visited;
    public:
        AdjacencyMatrix(int n);
        ~AdjacencyMatrix();
        void add_edge(int origin, int destin, int weight);
        void display();
        /* etc. */
};
```

Adjacency lists conserve more space by using lists of edges
stored at each vertex to represent adjacencies instead of an
n by n matrix. In an adjacency list we store a list for  
each node that contains the edges for that node. Each element
in that list represents an edge in the graph and contains
information such as the starting and ending vertices as well
as the edge weight. The image below illustrates this.
 

<img src="http://rosemary.umw.edu/~finlayson/class/spring13/cpsc230/notes/images/incidence.png"/>

Since we need to create nodes for the vertices and edges we can
now add other useful attributes to each vertex to help us with our
algorithms. For example, a color attribute for use with a graph
coloring algorithm or a visited attribute for a graph traversal
algorithm. The implementation consists of three classes; the 
`Adjacency_List` class, the `Vertex` class and the `Edge` class. 
If you notice in the example below, the Vertex class contains a list
of edges and the Edge class contains a pointer to both a starting 
and ending vertex.

```cpp
class Vertex{
    private:
        vector<Edge*> Adjacencys;
        int color;
        bool visited;
    public:
        Vertex();
        ~Vertex();
};

class Edge{
    private:
        Vertex *from;
        Vertex *to;
        int weight;
    public:
        Edge();
        ~Edge();
};

class AdjacencyList{
    private:
        vector<Vertex*> Vertices;
    public:
        Graph();
        ~Graph();
        void add_edge(Vertex *from, Vertex *to, int weight);
        void add_edge(int from, int to, int weight);
        void display();
        /* etc. */
};
```

DFS and BFS
-----------

Depth First Search (DFS) and Breadth First Search (BFS) are the two
primary search algorithms that all other algorithms use to  traverse
a graph. A depth first search will start at the given node and add
all of the unvisited adjacent nodes to a stack. It will then mark the current node as visited and repeat the process on the next node which it pops off of the stack. This process repeats until all of the vertices have been visited and the stack is empty. A breadth first search, on the other hand, starts at the given vertex and then adds all of its adjacent vertices to a queue. When this is complete, the algorithm marks the vertex as visited and moves on the the next vertex in the queue. It repeats this process until all of the vertices have been visited and and the queue is empty. The easiest way to remember these essential algorithms is to mentally link DFS to Stacks and BFS to Queues.

Exercise 1
-----------
Implement a Graph class using either the Adjacency Matrix or the
Adjacency list approach. Feel free to use the code given above
to help you get started.

Exercise 2
-----------
A cycle is any point in a graph where it is possible to travel in a
loop. For example; there is an edge from A to B, from B to C, and
from C back to A. Write a member function that detects whether your
graph contains any cycles and returns true or false respectively.


Exercise 3
-----------
Write a member function that, given a starting vertex and an ending
vertex, prints out a list of vertices that connect a path between
them.

Stretch-goal exercise:
----------------------
Can you come up with an algorithm that finds the shortest
path between two given vertices?

