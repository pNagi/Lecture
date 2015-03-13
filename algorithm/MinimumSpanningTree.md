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

| Minimum edge weight data structure | Time complexity (total) |
|---|---|
| adjacency matrix, searching	| `O(|V|2)` |
| binary heap and adjacency list	| `O((|V| + |E|) log |V|)` = `O(|E| log |V|)` |
| Fibonacci heap and adjacency list	| `O(|E| + |V| log |V|)` |

###3. Kruskal's Algorithm

###4. Reverse-delete algorithm
