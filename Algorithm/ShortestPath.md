#Shortest Path Problem

Given an **undirected weighted** graph,
G = (V, E, W) and given `source` node and `target` node.
For any `edge` e there is `weight` w[e] and w[e] >= 0.

Goal: Find the **minimum** weighted path from source to target

###Dijstra's Algorithm

#####Psuedo Code

    function Dijkstra(Graph, source):
        
        dist[source] ← 0                        // Distance from source to source
        prev[source] ← undefined                // Previous node in optimal path initialization
        
        for each vertex v in Graph:             // Initialization
            if v ≠ source                       // Where v has not yet been removed from Q (unvisited nodes)
                dist[v] ← infinity              // Unknown distance function from source to v
                prev[v] ← undefined             // Previous node in optimal path from source
            end if 
            add v to Q                          // All nodes initially in Q (unvisited nodes)
        end for
        
        while Q is not empty:
            u ← vertex in Q with min dist[u]    // Source node in first case
            remove u from Q 
            
            for each neighbor v of u:           // where v is still in Q.
                alt ← dist[u] + length(u, v)
                if alt < dist[v]:               // A shorter path to v has been found
                    dist[v] ← alt 
                    prev[v] ← u 
                end if
            end for
        end while
        
        return dist[], prev[]
        
    end function

[Credit: wiki](http://en.wikipedia.org/wiki/Dijkstra's_algorithm)

    S = {source}
    while (S != emptyset)
        u = ExtractMin(S)
        for every edge e = (u, x)
            if (d(u) + w[e] < d(x))             // อัพเดทถ้าเส้นทางที่มา + weight ใหม่ น้อยกว่า min ปัจจุบัน
                Update(d(x))                    // if new distance is smaller so we keep it
            end if
        end for
    end while
    
#####Big O

`O(|E| |decrease-key(Q)| + |V| |extract-min(Q)|)`

|  | Array | Sorted Array | Sorted LinkList | Heap |
|---|---|---|---|---|
| ExtractMin | `O(n)` | `O(1)` | `O(1)` | `O(nlog(n))` |
| Update | `O(1)` | `O(n)` | `O(n)` | `O(mlog(n))` |
| TOTAL | `O(n^2)` | `O(mn)` | `O(mn)` | `O(mlog(n))` CHECK PLS |

สรุป `Heap` เร็วสุด
+ Fibonacci heap: `O(|E| + |V| log |V|)`
+ binary heap: `O((|E| + |V|) log |V|)`
+ unsorted array: `O(|V|^2)`
