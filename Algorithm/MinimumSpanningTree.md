Every connected graph has spanning tree
Note that if all edges are distinct = easier to proof

#Minimum Spanning Tree

Given an weighted directed graph G = (V, E, W)
There is weight w[e] on edge

Goal: Find Minimum-cost spanning tree

Def: Spanning Tree is a tree that contains all nodes

Ex.
+ BFS/DFS tree
+ Shortest Path Tree

##Way to find MST

###1. Borůvka's algorithm
อาจารย์ไม่ได้สอน

###2. Prim's Algorithm

[GREAT NOTES!](https://www.cse.ust.hk/~dekai/271/notes/L07/L07.pdf)

    Make a queue (Q) with all the vertices of G (V);
    For each member of Q set the priority to INFINITY;
    Only for the starting vertex (s) set the priority to 0;
    The parent of (s) should be NULL;
    While Q isn’t empty
        Get the minimum from Q – let’s say (u); (priority queue);
        For each adjacent vertex to (v) to (u)
            If (v) is in Q and weight of (u, v) < priority of (v) then
                The parent of (v) is set to be (u)
                The priority of (v) is the weight of (u, v)

psuedo code

    source = randomly pick
    key[source] ← 0
    prev[source] ← undefined
    pass[source] ← false
    
    for each vertex v in Graph:             // Initialization
        if v ≠ source                       // Where v has not yet been removed from Q (unvisited nodes)
            key[v] ← infinity              // Unknown weight from source to v
            pass[v] ← false                 // Node is not passed
        end if
        add v to Q                          // All nodes initially in Q (unvisited nodes)
    end for
    
    while Q is not empty:
        u = Q.extractMin()                  // Source node in first case
        remove u from Q
        
        for each neighbor v of u:           // where v is still in Q.
            if !pass[v] && weight(u, v) < key[v]:
                key[v] ← weight(u, v)
                Q.decreaseKey(v, key[v])
                prev[v] ← u
            end if
            pass[u] = true;
        end for
    end while
    
| Minimum edge weight data structure | Time complexity (total) |
|---|---|
| adjacency matrix, searching	| `O(|V|2)` |
| binary heap and adjacency list	| `O((|V| + |E|) log |V|)` = `O(|E| log |V|)` |
| Fibonacci heap and adjacency list	| `O(|E| + |V| log |V|)` |

[psuedo code](http://www.stoimen.com/blog/2012/11/19/computer-algorithms-prims-minimum-spanning-tree/)
[prim's algorithm running time analysis](https://www.cse.ust.hk/~dekai/271/notes/L07/L07.pdf)

Queue          |  T_e   |  T_d   |  T_k   | w/o Dec-Key |   w/Dec-Key
---------------|--------|--------|--------|-------------|---------------
Binary Heap    |O(log N)|O(log N)|O(log N)| O(M log N)  |   O(M log N)
Binomial Heap  |O(log N)|O(log N)|O(log N)| O(M log N)  |   O(M log N)
Fibonacci Heap |  O(1)  |O(log N)|  O(1)  | O(M log N)  | O(M + N log N)

T_e = enqueue
T_d = dequeue
T_k = decrease key

[credit: stackoverflow](http://stackoverflow.com/questions/9255620/why-does-dijkstras-algorithm-use-decrease-key)

###3. Kruskal's Algorithm

    KRUSKAL(G):
    A = ∅
    foreach v ∈ G.V:
        MAKE-SET(v)
    sort the edges of G.E into nondecreasing order be weight(u, v)
    foreach edge ordered by weight(u, v):
        if FIND-SET(u) ≠ FIND-SET(v):
            A = A ∪ {(u, v)}
            UNION(u, v)
    return A

###4. Reverse-delete algorithm
