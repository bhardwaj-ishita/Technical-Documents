# graphs:

it has edges and vertices (Graph<N,E>)

vertices: nodes that store the info

edges: the path between two vertices/nodes

both are finite

![image-20210722140816577](C:\Users\ayush\AppData\Roaming\Typora\typora-user-images\image-20210722140816577.png)

N={0,1,2,3,4,5,6} (set of nodes)		E={01,12,23,34,45,05,03} (set of edges)

## types of graphs:

#### 1. weighted

whose edges or paths have values.
ex:   distance between two offices 
		the speed from one data packet in the network to another

#### 2. unweighted

no value is associated to the edges

#### 3. undirected

![image-20210722142612752](C:\Users\ayush\AppData\Roaming\Typora\typora-user-images\image-20210722142612752.png)

here all the edges are bidirectional and both nodes can pass information to each other

#### 4. directed

![image-20210722142558819](C:\Users\ayush\AppData\Roaming\Typora\typora-user-images\image-20210722142558819.png)

here one node is connected  and directed from one node to another 

## storing of graph:

#### adjacency list

![image-20210722143222557](C:\Users\ayush\AppData\Roaming\Typora\typora-user-images\image-20210722143222557.png)

nodes are stored as an index of 1-d array 
edges are stored as list in that index

#### adjacency matrix

![image-20210722172203879](C:\Users\ayush\AppData\Roaming\Typora\typora-user-images\image-20210722172203879.png)

diagonally symmetrical 

at each index defines the node and the 1s in that row/column defines the connected nodes and all the other default values are 0s

## graph traversal:

searches for edges without making a loop. when visited a node, it is marked so it is not visited again

#### dfs (depth first)

starts from one node and goes deeper towards one path and then come back and goes deeper to another path

for connected graph, visit the paths deep first from the root

for disconnected graph, after the dfs from one node, do the dfs for all the unvisited nodes.

Time complexity O(V+E)

Space complexity O(V)

#### bfs (breadth first)

starts from one node and goes to all the edges of that particular node and then goes to the edges(children) of the visited nodes

Time complexity O(V+E)

Space cop